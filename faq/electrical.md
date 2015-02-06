---
layout: page
title: Electrical FAQ
permalink: /faq/electrical/
---


##How do I wire up the control system?
FIRST provided a great picture in one of their blogs, showing a typical wire diagram for the new 2015 control system, reposted below:

The one thing that is missing is the D-link, which would plug into the VRM for power, and connect to the roboRIO via Ethernet cable.

This diagram still shows the early thought of using a USB Bridge directly plugged into the roboRIO (which was scraped after alpha testing and replaced by using the trusted D-link)

<img src="../../Images/2015_CS_Layout.jpg">

---

##What wire should I use for the new weidmuller connectors?
Refer to the official FRC rules for specific wiring requirements, however with that said,

We have had a lot of success using 18 awg  "outdoor security wire". These typically come with thin walled jackets and you can find them in shielded or non-shielded varients. The wire we used during beta testing we bought at home depot [18 awg security wire](http://www.homedepot.com/p/Southwire-18-2-Shield-Security-Cable-By-the-Foot-57573199/204725192?N=5yc1vZc7d4).
<br><br>

* We use 18-2 wire for all control system interconnects (power and CAN) 
* We use 6 awg battery cables
* We use 22-2 cable for PWM cables (no center wire needed), solenoid wires, and 5 V sensors 

We buy our wires in singles and spin our own lengths from this site: http://www.mcmelectronics.com/content/en-us/landing_pages/hook-up-wire


---
