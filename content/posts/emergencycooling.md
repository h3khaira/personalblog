+++
title = 'Sizing Emergency Cooling Exhaust Fans'
date = 2024-06-18T21:22:35-04:00
draft = false
description = "Here I describe how I size emergency cooling exhaust fans."
toc = false
readTime = true
math = true
tags = ["mini-hub", "HVAC", "emergency cooling"]
showTags = false
hideBackToTop = false
+++
During my work I run into client requirements where the client requires an emergency ventilation system in a critical electrical or communication room. This system is meant to turn on when the main air conditioning system in this room becomes non-functional for whatever reason in the summer. Since these rooms tend to contain critical infrastructure, they must never be brought offline, which means the equipment is always generating heat.

In this scenario, we don't want the room temperature to get too high while the A/C is being repaired. Therefore, we design an emergency cooling exhaust fan that replaces in the room air with outside air to keep the temperature at some reasonable setpoint. 

## Calculation
In order to size the emergency cooling exhaust fan, we need to know a few parameters:
1. The heat dissapation in the room in Btu/hr. We will represent this with the symbol $Q$.
2. The internal temperature setpoint. Typically we keep this around 38&deg;C (100&deg;F).  We represent this with the symbol T~i~.
3. The external temperature. For this we go with the worst case scenario, which according to OBC is around 31&deg;C in Toronto. We represent this with the symbol T~o~

With these factors determined, the airflow can be calculation in cubic foot per minute (CFM) according to the following formula:
$$
CFM [\frac{ft^3}{min}]= \frac{Q [\frac{Btu}{hr}]}{1.08(To [&deg;F]-Ti[&deg;F])}
$$

Equipped with this airflow, we can then proceed to size the exhaust fan to provide emergency cooling.