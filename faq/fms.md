---
layout: page
title: Field Management System (FMS) FAQ
permalink: /faq/fms/
---

##What's new with FMS for 2015?

The network setup being tested for the 2015 system is a little bit different than the previous Control System. The new scheme utilizes mDNS to allow for the use of DHCP addressing and seamless transition from ethernet to USB and back.

###What is mDNS?
Multicast Domain Name System (mDNS) is a system which allows for resolution of host names to IP addresses on small networks with no dedicated name server. To resolve a host name a device sends out a multicast message to the network querying for the device. The device then responds with a multicast message containing it's IP. Devices on the network can store this information in a cache so subsequent requests for this address can be resolved from the cache without repeating the network query.

The FRC Driver Station, LabVIEW, and the Eclipse plugins for C++ and Java are all programmed to discover your roboRIO using the mDNS protocol. This means that the roboRIO can be detected regardless of the interface or IP being used.

To use mDNS on FRC, a mDNS resolver must be installed on your development computer.

* Windows
  - mDNS resolver is installed with NI/FIRST software
  - iTunes uses mDNS and installs a resolver if your windows machine has iTunes.
* Linux
  - Most Linux distros have a mDNS resolver installed by default such as Ubuntu or Mint, if not
  - Install nss-mDNS or Avahi or Zeroconf
* Apple
  - Apple Bonjour is a mDNS resolver and is installed in OSX by default


Most web-browsers should be able to utilize the mDNS address to access the roboRIO webserver as long as an mDNS provider is installed. Please note the following exceptions:

Chrome - In Google Chrome, a trailing '/' must be appended to access mDNS addresses (eg.  roboRIO-190.local/)

###How do I set up my Robot Network to use mDNS?
USB
If using the USB interface, no setup is required. The roboRIO driver will automatically configure the IP address of the host (your computer) and roboRIO and the software listed above should be able to locate and utilize your roboRIO

Ethernet/Wireless
The 2015 Bridge Configuration Utility has been modified to enable the DHCP server on the DAP1522 radio in the home use case (AP mode), if you are putting the DAP1522 in bridge mode and using a router you can enable DHCP addressing on the router. The bridge is set to the same team based IP address as before (10.TE.AM.1) and will hand out DHCP address from 10.TE.AM.20 to 10.TE.AM.199

RoboRIO Ethernet Configuration
The roboRIO Ethernet interface should be set to DHCP. When connected to the DAP1522 bridge, the roboRIO will receive an IP from the bridge. When tethered directly to a PC, both devices will self-assign IPs.

PC  Configuration
When connecting via Ethernet (to either the radio or directly to the roboRIO) or Wireless (to the DLink radio), your computer adapter should be set to DHCP. When connecting through the DAP1522, your PC will receive an IP address from the radio. If tethered directly to the roboRIO both devices will self-assign IPs.

mDNS works on the field such that all of your devices are located using their mDNS address so static IPs are no longer required.

---

##mDNS IP Lists

IPs for system components:

roboRIO USB: 172.22.11.2

roboRIO mDNS: roboRIO-####.local (where #### is your team number with no leading zeroes) You should be able to use this address to communicate with the roboRIO over either interface through ping, browser, etc.

Robot Radio: 10.TE.AM.1 (where TE.AM is your 4 digit team number with leading zeroes if required)
roboRIO Ethernet: DHCP, assigned by the Robot Radio
Driver Station PC: DHCP, assigned by the Robot Radio
Additional Programming computers: DHCP, assigned by the Robot Radio

DHCP range: 10.TE.AM.20 to 10.TE.AM.199

Note: You can still assign static IPs to any device on the Robot. However, do so between 10.TE.AM.2 and 10.TE.AM.19 so as to not interfere with the DHCP addressing on the of the field.

---

##Can I still stream images/Video to the Driver Station?
Yes, however remember the Link between the driverstation and the Robot is capped at 7 Mbits/second total. The Driverstation protocol uses roughly 900kbits/sec alone, leaving ~6Mb/s for any network tables, camera traffic, or any other data the team wishes to transmit over the WIFI network. As a Control Engineer, I would recommend teams ensure that at no time are they using more than 5Mb/s total (including DS packets) to maintain reliable connection. More information on FMS can be learned from the FMS whitepaper released by FIRST: [FMS Whitepaper](http://www.usfirst.org/sites/default/files/uploadedFiles/Robotics_Programs/FRC/Game_and_Season__Info/2013/FMSWhitePaper_RevA.pdf)

FIRST also released a FMS light program so teams can practice at home, with a similar FMS in the loop. However, FMS Lite is not FMS and there is no guarantee that your performance during tests will be mirrored during a competition. [FMS Lite](http://www.usfirst.org/roboticsprograms/frc/blog-2014-fms-lite-available)
