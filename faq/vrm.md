---
layout: page
title: Voltage Regulator Module (VRM) FAQ
permalink: /faq/vrm/
---

##Specs: 
5V Rail and 12V Rail
Input power: 4-12V

##What kind of converter is the VRM?
The VRM is a buck-boost converter.

---

##How many Amps can the VRM Source?
At No time can the user draw more than 2.0A peak from any/all 12V regulated channels
At No time can the user draw more than 2.0A peak from any/all 5V regulated channels

Each rail is split into a 0.5A Max set of channels, and a 2A Max set of channels. At no time can the user exceed that current limit on the pair of channels. 

Under stress testing, most teams observed it is best to keep the current draw of each rail below 1.5A continuous so as to not enter a fault condition on the VRM.

---

##Can I power the D-Link from the VRM?
Yes, but check 2015 rules. One caveate, the D-link manufacture spec state the DAP-1522 requires 2A @ 5VDC. I would recommend teams to not plug any other 5V device into the same VRM they are using to power the D-Link radio. The VRM is limited to 2.5 amps on the 5V rail, and you do not want anything (such as a camera, or off-board processor) robbing current from the Radio. If you loose power to the radio, you loose communications during a match. If you must power other 5V devices, use another FIRST approved regulator, or use a second VRM. It is safe to use the 12V rail to power another device from the same VRM that powers the D-link because the 12V and 5V are isolated.

