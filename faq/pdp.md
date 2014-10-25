---
layout: page
title: Power Distribution Panel (PDP) FAQ
permalink: /faq//pdp/
---

##What is sample rate of current monitoring?
The currents are put out on CANbus once every 25ms.

---

##What does the PDP monitor over CAN?
Correct. Only the main 16 power channels have current monitoring. 

---

##When we remove a 40A circuit breaker from the Power Distribution Board, we are having some difficulty. 
These are the exact same fuse holders used on the existing PD.  I noticed that the first time the breaker is inserted it
 is a bit more difficult than subsequent insertions.  This has always been my experience even with the current design.  


Unfortunately there are not many options when it comes to this type of fuse holder. 

---

##Would someone be able to confirm whether or not the VRM/PCM/RoboRIO ports have current monitoring? ie Do the three ports along the bottom of the PDP have current monitoring like the rest of the panel?

The PDP does not monitor those dedicated power outputs directly.
 The PDP does monitor:The current outputs of each (16) of the high power draw wago connectors
Short circuits detected on each of the (16) wago connectors
The incoming battery voltage
The internal PDP temperature
Any over-temperature fault
The PCM monitors compressor current, and faults for shorts and compressor over-current.

---

