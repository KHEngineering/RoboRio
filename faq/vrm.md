---
layout: page
title: Voltage Regulator Module (VRM) FAQ
permalink: /faq/vrm/
---

<img src = "../../Images/vrminfo.png">

##Specs: 
5V Rail and 12V Rail
Input power: 4-12V

##What kind of converter is the VRM?
The VRM is a [buck-boost converter](http://en.wikipedia.org/wiki/Buck%E2%80%93boost_converter).

---

##How many Amps can the VRM Source?
At no time can the user draw more than 2.0A peak from any/all 12V regulated channels
At no time can the user draw more than 2.0A peak from any/all 5V regulated channels

Each rail is split into a 0.5A Max set of channels, and a 2A Max set of channels. At no time can the user exceed that current limit on the pair of channels. 

> Note: Under stress testing, most Beta teams observed it is best to keep the current draw of each rail below 1.5 Amps continuous so as to not enter a fault condition on the VRM. Therefore our recommendation would be to make sure you keep the current draw below 1.5 Amps total for each rail (5V or 12V).

---

##Can I power the D-Link from the VRM?
Yes, but check 2015 rules for official wiring. One caveat, the D-link manufacture spec states that the DAP-1522 requires 2A @ 5VDC. I would recommend that teams not plug any other 5V device into the same VRM they are using to power the D-Link radio. The VRM is limited to ~2.0 amps on the 5V rail, and you do not want anything (such as a camera, or off-board processor) robbing current from the radio. If you lose power to the radio, you lose communications during a match. 

If you must power other 5V devices, use another FIRST approved regulator, or use a second VRM. It is safe to use the 12V rail to power another device from the same VRM that powers the D-link because the 12V and 5V are isolated.

---

##Can I use another regulator
Refer to the official rules for the answer to this question.
[Competition Manual](http://frc-manual.usfirst.org/) "Competition Manual")

---

##How can I wire a second VRM?
Refer to the official rules for the answer to this question. Beta teams have been sucessfully wiring additial VRM and PCM modules to spare 30A unregulated channels on the PDP.
[Competition Manual](http://frc-manual.usfirst.org/) "Competition Manual")

---

##Can I montior the VRM over CAN?
No the VRM is not a CAN device, it is simply a regulated supply and provides no feedback other than the LED status light on the device.

---

##What do the LEDs on the VRM indicate?
When the VRM is powered properly (12 volts input), the 12V and 5V LEDs should be green indicating that circuit is operation.

