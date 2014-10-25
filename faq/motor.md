---
layout: page
title: Motor Controller FAQ
permalink: /motor/
---

##Can I still use the Black and Tan Jaguars?
The system should support either jag with the latest firmware (v107 for black, v101 for grey). Using a mix would be 
great for testing purposes.

---

##Do Talons and Victors still have limited resolution compared to Jaguars?
The overall PWM resolution has been increased (from ~8 bits to ~11) but Jaguars still, by default, use a wider input 
range than Victors or Talons and thus will have a finer resolution. 
The cRIO through the NI 9403 has a resolution of 6.525 us between updates to the PWM signals.
The roboRIO has a resolution of 1 us between updates to the PWM signals.  The only reason the "bits of resolution" went 
up (that Kevin mentioned) was to make sure the whole range could still be covered at the new smaller period between 
updates.

---

The 3.3v/5v internal jumper only affects the DIO power output.
 The PWM signals are always 5v max.
 The PWM power is always 6v. The motor controllers have this line disconnected, so power on it doesn't affect them.

---

Right....I would like to see the 6V signal when the servos is trying to move a high inertia mass. I am guessing the 6V signal will drop from 5.7 to below 5.0  when there is a load on the servo. Can some of you RoboRIO owners try that ? We are designing a PWM extender (for servos and motors) that needs the 6V supply to stay above 5.3V.

 Thanks,
 
Fear not. This is an artifact of the back-drive protection on this supply. The current path passes through a diode when the load is low. When the current is detected to be enough greater than 0, a FET is switched on and the diode is bypassed. This means that at no load the output looks low, but as soon as there is a load, the voltage climbs to 6V.

 Please see the attached image. This is a graph created using the new Power palette in WPILib (that's right, you can monitor this directly in the controller without external connections). I plugged in a servo, enabled, and then twisted the output shaft with my hand, forcing it to fight me and increase load on the power supply. You can see that under load the voltage increases, not decreases.
 