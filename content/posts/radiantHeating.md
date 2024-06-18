+++
title = 'Radiant Floor Heating Systems in GO Stations'
date = 2024-06-17T19:09:49-04:00
description = "A writeup on the functionality of a radiant floor heating system."
draft = false
math = true
+++
## What is it?
According to the GO DRM, all conditioned spaces inside of a GO station must be heated by a radiant floor heating system. This includes spaces such as the ambassador office, washrooms, retail space etc. However, this does not include auxillary spaces such as mechanical or electrical rooms. For more detail, refer to DS-04.

Now what is a radiant floor heating system? In summary: it consists of heating a space by circulating hot water through pipes embedded in the floor slab, thus raising the slab temperature. This heats the room in two ways:
1. Natural convection
2. Thermal radiation

The system works to maintain the slab temperature at 37.5&deg;C by circulating hot water through the loops.

The specific Metrolinx requirements for a radiant floor heating system can be found [here.](https://www.gosite.ca/engineering_public/standard_drawings/Mechanical%20Drawings%20and%20Specs/23%2021%2012%20Hydronic%20Radiant%20Floor%20Heating%20System.pdf)

## Components
There are several components that are common for all radiant floor heating systems.
1. Boilers: Typically a system will consist of two boilers to heat the water circulating through the pipes. These boilers will be sized to ~65% of the total load so they can be staged on and off.
2. Boiler pumps: We typically have one pump dedicated per boiler so that the water can be circulated through the boiler.
3. Main loop pumps: Then we have the pumps that circulate hot water through the main loop. Typically, we will have N+1 redundancy for these pumps.
4. Mixing valve: After the main loop pumps, we typically provide a mixing valve. This valve modulates to mix the supply and return side of the loops to maintain a specified loop temperature.
5. Mixing header: Then we have a main header that will distribute piping to the manifolds located in each zone being served by the system.
6. Manifold cabinets: Finally, we have manifold cabinets distributed throughout the system that distribute hot water through loop piping into the slabs. Each cabinet can serve multiple zones.
7. Slab temperature sensors: As the name suggests, these sensors measure the slab temperature to allow for precise control of the system.
