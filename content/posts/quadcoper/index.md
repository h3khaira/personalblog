+++
title = 'The STM32 Blue Pill DIY Quadcoper'
date = 2024-07-17T18:06:02-04:00
draft = false
summary = "A drone flight controller using the STM32F103 Blue Pill. This project is heavily influenced by Joop Brokking."
description = "Here I go through a summary of the quadcopter controller I have been working on for a while. "
toc = false
readTime = true
autonumber =false
math = true
tags = ["project", "educational"]
showTags = false
hideBackToTop = false
+++

A drone flight controller using the STM32F103 Blue Pill. This project is heavily influenced by Joop Brokking, whose project can be found here [on his youtube channel.](https://www.youtube.com/watch?v=MLEQk73zJoU&t=51s)

# Components
![drone picture](./images/drone.jpg)

This drone uses a generic F450 drone frame as the main platform. The motors are four (4) 1000 KV rated motors from aliexpress.

The brain of the drone is the STM32F103 "Blue pill" controller pictured above. The drone also uses a generic MPU6050 module for its orientation measurements. The drone also uses some LEDs for error signals as well as a generic SSD1306 OLED display module. A summary of the components for this drone are listed below.

| Item                 | Name                                               |
------------------------------|-----------------------------------------------
| Controller           | STM32F103C8T6 'Blue Pill'                          |
| IMU                  | MPU-6050                                           |
| Frame                | F-450 Generic                                      |
| Motors               | QWinOut 1000 KV motors                             |
| Speed Controller     | Generic 30A Electronic Speed Controller            |
| Battery              | Generic 3 cell lipo battery                        |
| OLED Display         | SSD1306 OLED Display Modules                       |
| Transmitter/Receiver | Hobby King 2.4 GHz HK T6A V2 6-channel transmitter |

# Development Platform

I decided to use platformIO for developing the code for this project, with the arduino and stm32duino tools. The platfomio.ini content I used is listed below.

By default the blue pill boards require a debugger such as an ST-LINK for flashing and debugging. However, there is luckily a bootloader available that allows for flashing and debugging using the USB serial ports like a standard Arduino.

```
[env:bluepill_f103c8]
platform = ststm32
board = bluepill_f103c8
upload_protocol = hid
upload_port = /dev/ttyACM0
framework = arduino
monitor_speed = 57600
board_build.core = stm32duino
build_flags =
	-D PIO_FRAMEWORK_ARDUINO_ENABLE_CDC
	-D USBCON
	-D USBD_VID=0x0483
	-D USBD_PID=0x5740
	-D USB_MANUFACTURER="Unkown"
	-D USB_PRODUCT="\"BLUEPILL_F103C8\""
	-D HAL_PCD_MODULE_ENABLED
monitor_dtr = 1
lib_deps =
	adafruit/Adafruit GFX Library@^1.11.5
	adafruit/Adafruit SSD1306@^2.5.7
```

# Hardware Interaction
## MPU-6050 IMU
Communication to the MPU-6050 module is done using the following code snippet:

```
  void startGyro()
{
  Wire1.beginTransmission(gyroAddress);
  Wire1.write(0x6B); // power management register
  Wire1.write(0x00); // setting this bit wakes up the MPU-6050 module
  Wire1.endTransmission();

  Wire1.beginTransmission(gyroAddress);
  Wire1.write(0x1B); // Access the GYRO_CONFIG register
  Wire1.write(0x08); // Write the FS_SEL bits to change gyro resolution to 500 degrees per second, 1 DEG/SEC  = 65.5 OUTPUT FROM GYRO LSB (check page 31 of manual)
  Wire1.endTransmission();

  Wire1.beginTransmission(gyroAddress);
  Wire1.write(0x1C); // Access accelerometer config register
  Wire1.write(0x10); // Set the AFSL bit +-8g = 4096 LSB/g
  Wire1.endTransmission();

  Wire1.beginTransmission(gyroAddress);
  Wire1.write(0x1A); // Access CONFIG register
  Wire1.write(0x03); // Digial Low Pass Filter for gyro/accelorometer set to 43 Hz
  Wire1.endTransmission();
}
```

The I2C address for this module is 0x68. Arduino contains the library "twowire" for I2C communication, which we use to interact with the data registers of MPU-6050. The register map for the MPU-6050 can be found [here](https://invensense.tdk.com/wp-content/uploads/2015/02/MPU-6000-Register-Map1.pdf)
We first, wake up the MPU-6050 module, configure the resolution of the gyroscope and accelerometer measurements, and apply the in-built digital low pass filter to reduce the noise in the measurements.

## Hardware Timers, Pulse Width Modulation, Interrupts and Working with Receivers
In order to interact with the motors and receivers with the stm32, we need to work with the hardware timers included on this board. The stm32 board has four (4) hardware timers built-in.

The stm32 has a main clock speed of 72 MHz, so we set the prescaler value to 72 to allow our timers to reset at 1 MHz.

Looking at the register map for STM32, we can see that timers TIM2 to TIM8 are general purpose timers, so we will be using those timers for our use-case. These timers can be used to either capture input pulse lengths, or to output pulses of specified length.

We know that the receiver outputs signals in terms of pulse lengths. We also know that motor speed control is achieved through pulse length modulation. Therefore, this is the perfect use case for hardware timers. We initialize timer 2 and timer 3 for handling the receiver inputs, and timer 4 to serve as the PWM output to control the motors.

### Receiver Interrupts
The receiver pins are connected to pins A0 to A3 and A6, A7 on the blue pill. The blue pill pinout diagram shows that A0 to A3 are connected to hardware timer 2 and pins A6 and A7 are connected to timer 3. We will utilize the input capture mode on these timers to detect when the receiver sends a pulse into each pin and generate an interrupt.

The input capture mode works by using the CCLR register to detect rise and falling edges of a pulse. For each time a falling/rising edge is detected, the capture compare register CCR1 is populated by the value of the counter register CNT. An interrupt is then generated through the DIER register which can be handled by an interrupt handler. By comparing the time between the rising and falling edges, the length of the pulse can be determined. This pulse length represents the states of the throttle, pitch/roll level, etc on the transmitter.

The setting of registers in C++ is done using the following code as an example:
```
  TIM3->DIER = TIM_DIER_CC1IE | TIM_DIER_CC2IE; // capture/compare 1,2 interrupt enable
```
In this case, the CC1IE and CC2IE bits are set in the DIER register to enable the interrupt.
### Controlling Motor Speeds
The motor speed is controlled by sending the electronic speed controller a square pulse of a length between 1000-2000 microseconds, where 1000 microseconds indicates 0% speed and 2000 indicates 100% speed. Before the motors can be controlled, they need to be initialized by sending them a pulse of 1000 microseconds after power on. Without a microcontroller, this is done by moving the throttle into a "0" position. We will do so by sending each motor one pulse of 1000 microseconds at the start of our program.

The motors are connected to pins B6-B9, which are dedicated to Timer 4 channels 1-4. Therefore, we will need to set up this timer for us to interact with these motors. We will set these pins up in "PWM" mode according to the STM32 manual. This is done by setting the OCM bits according to the following code:

```
  TIM4->CCMR1 = 0b0110100001101000;// setting OC2M and OC1M bits to 110, also setting OC2PE and OC1PE bits to 1
  TIM4->CCMR2 = 0b0110100001101000;
```

We can then directly indicate the length of pulse we want to send to each motor. For instance; the code snippet below shows how to initialize all four motors by sending a 1000 microsecond pulse.
```
  TIM4->CCR1 = 1000; // register value here determines the pulse length, a 1000 microsecond length here initializes the motors
  TIM4->CCR2 = 1000;
  TIM4->CCR3 = 1000;
  TIM4->CCR4 = 1000;
```
# Controller
A quadrocopter is inherently an unstable system. Without some form of active control it cannot fly, as even a tiny deviation in the system such as one motor being slightly faster than the other cause the device to crash. Therefore, we need to provide active management of the inputs into the motors. We can do this by using a PID controller.

The idea is that we take the measurements coming in from our IMU (the MPU6050 module), do some math with them, incorporate them with the input coming in from the transmitter/receiver (and therefore the pilot) and then provide inputs to each motor to achieve the desired effect.
