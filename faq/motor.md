---
layout: page
title: Motor Controller FAQ
permalink: /faq/motor/
---

<img src = "../../Images/motorcontrollers.png">


##Can I still use the Black and Tan Jaguars?
The system should support either jag with the latest firmware (v107 for black, v101 for grey).

---

##I Accidently supplied power to the Motor Controller with reversed polarity, did I break it?
Possibly. The Talon,Talon SR, Victor 884, Victor 888, Black Jaguar or Tan Jaguars models DO NOT have reverse polarity protection. It may not fail immediately, but can fail over time. One should always be cautious when wiring a motor controller, the labels for each terminal are clearly marked. Review all wiring before powering any motor controller to ensure that they are wired correctly, and that power is being supplied to the proper terminals, in the proper polarity. 

---

##I Accidently supplied 12V power to the output side of the Motor Controller, did I break it?
Possibly, supplying unregulated power to the output of the Talon, Talon SR, Victor 884, Victor 888, Black Jaguar, or Tan Jaguar models may permenantly damage the H-bridge inside of the device. The device may not fail immediately, but can fail over time.

---

##Do Talons and Victors still have limited resolution compared to Jaguars?
The overall PWM resolution has been increased (from ~8 bits to ~11) but Jaguars still, by default, use a wider input 
range than Victors or Talons and thus will have a finer resolution. 
The cRIO through the NI 9403 has a resolution of 6.525 us between updates to the PWM signals.
The roboRIO has a resolution of 1 us between updates to the PWM signals.  The only reason the "bits of resolution" went 
up (that Kevin mentioned) was to make sure the whole range could still be covered at the new smaller period between 
updates.

---

##Do I need to set the internal jumper on the RoboRio to drive Servos?
No. The 3.3v/5v internal jumper only affects the DIO channel power output.
The PWM signals are always 5v max. The PWM power is always 6v output. The motor controllers have this line disconnected, so power on it doesn't affect them. This means you can use the same PWM pins to power 6V servos, or FRC legal motor controllers without changing any hardware settings.

---

##I measured the 6V rail, and it is actually 5.7V. I am guessing the 6V signal will drop from 5.7 to below 5.0  when there is a load on the servo. 

Fear not. This is an artifact of the back-drive protection on this supply. The current path passes through a diode when the load is low. When the current is detected to be greater than 0, a FET is switched on and the diode is bypassed. This means that at no load the output looks low (5.7V), but as soon as there is a load, the voltage climbs to 6V.

Please see the attached image. This is a graph created using the new Power palette in WPILib (that's right, you can monitor this directly in the controller without external connections). I plugged in a servo, enabled, and then twisted the output shaft with my hand, forcing it to fight me and increase load on the power supply. You can see that under load the voltage increases, not decreases.
 
---

##Can I use the Talon SRX in PWM or CAN mode?

Yes, the talon SRX will automatically detect whether it is connected to a PWM source or a CAN source

