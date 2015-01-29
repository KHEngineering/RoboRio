---
layout: page
title: Field Management System (FMS) FAQ
permalink: /faq/fms/
---

##What's new with FMS for 2015?

The network setup being tested for the 2015 system is a little bit different than the previous control system. The new scheme utilizes mDNS to allow for the use of DHCP addressing and seamless transition from Ethernet to USB and back.

There is also a new 2015 protocol which uses less bandwidth for DS to robot communications.

---

##What is mDNS?
Multicast Domain Name System (mDNS) is a system which allows for resolution of host names to IP addresses on small networks with no dedicated name (DNS) server. To resolve a host name a device sends out a multicast message to the network querying for the device. The device then responds with a multicast message containing it's IP. Devices on the network can store this information in a cache so subsequent requests for this address can be resolved from the cache without repeating the network query.

Basically, instead of having to know the IP address of every device on your network, you can communicate with them using their mDNS name (something like "ping roborio-2168.local" instead of "ping 10.21.68.2"

The FRC Driver Station, LabVIEW, and the Eclipse plugins for C++ and Java are all programmed to discover your roboRIO using the mDNS protocol. This means that the roboRIO can be detected regardless of the interface or IP being used.

To use mDNS on FRC, a mDNS resolver must be installed on your development computer.

* Windows
  - mDNS resolver is installed with NI/FIRST software
  - iTunes uses mDNS and installs a resolver if your Windows machine has iTunes.
* Linux
  - Most Linux distros have a mDNS resolver installed by default such as Ubuntu or Mint, if not
  - Install nss-mDNS or Avahi or Zeroconf
* Apple
  - Apple Bonjour is a mDNS resolver and is installed in OSX by default


Most web-browsers and applications should be able to utilize the mDNS address to access the roboRIO webserver as long as an mDNS provider is installed. 

For example: you should be able to navigate to http://roborio-2168.local from any browser, or application requiring a hostname (like Putty, or Filezilla).

Please note the following exceptions:

Chrome - In Google Chrome, a trailing '/' must be appended to access mDNS addresses (eg.roboRIO-2168.local/)

---

##How do I set up my Robot Network to use mDNS?

* USB
If using the USB interface, no setup is required. The roboRIO driver will automatically configure the IP address of the host (your computer) and roboRIO and the software listed above should be able to locate and utilize your roboRIO

* Ethernet/Wireless
The 2015 Bridge Configuration Utility has been modified to enable the DHCP server on the DAP1522 radio in the home use case (AP mode), if you are putting the DAP1522 in bridge mode and using a router you can enable DHCP addressing on the router. The bridge is set to the same team based IP address as before (10.TE.AM.1) and will hand out DHCP address from 10.TE.AM.20 to 10.TE.AM.199

* RoboRIO Ethernet Configuration
The roboRIO Ethernet interface should be set to DHCP. When connected to the DAP1522 bridge, the roboRIO will receive an IP from the bridge. When tethered directly to a PC, both devices will self-assign IPs.

* PC  Configuration
When connecting via Ethernet (to either the radio or directly to the roboRIO) or Wireless (to the DLink radio), your computer adapter should be set to DHCP. When connecting through the DAP1522, your PC will receive an IP address from the radio. If tethered directly to the roboRIO both devices will self-assign IPs.

mDNS works on the field such that all of your devices are located using their mDNS address so static IPs are no longer required.

---

##mDNS IP Lists

IPs for system components:

- roboRIO USB: 172.22.11.2
- roboRIO mDNS: roboRIO-####.local (where #### is your team number with no leading zeroes) You should be able to use this address to communicate with the roboRIO over either interface through ping, browser, etc.
- Robot Radio: 10.TE.AM.1 (where TE.AM is your 4 digit team number with leading zeroes if required) (This is the address set by the FRC Bride Configuration Tool)
- roboRIO Ethernet: DHCP, assigned by the Robot Radio
- Driver Station PC: DHCP, assigned by the Robot Radio
- Additional programming computers: DHCP, assigned by the Robot Radio (DHCP range: 10.TE.AM.20 to 10.TE.AM.199)

Note: You can still assign static IPs to any device on the robot. However, do so between 10.TE.AM.2 and 10.TE.AM.19 so as to not interfere with the DHCP addressing on the of the field.

---

##Can I still stream images/Video to the Driver Station?
Yes, however remember the link between the driverstation and the robot is capped at 7 Mbits/second total. The 2014 Driverstation protocol uses roughly 900kbits/sec alone, leaving ~6Mb/s for any network tables, camera traffic, or any other data the team wishes to transmit over the WIFI network. As a Control Engineer, I would recommend that teams do not use more than 5Mb/s total (including DS packets) to maintain reliable connection. More information on FMS can be learned from the FMS whitepaper released by FIRST: [FMS Whitepaper](http://www.usfirst.org/sites/default/files/uploadedFiles/Robotics_Programs/FRC/Game_and_Season__Info/2013/FMSWhitePaper_RevA.pdf)

NI states the new 2015 protocol should only use about 90kbits/sec vs the 900kbits/sec of the 2014 protocol, so this should give more headroom for users wishing to utilize the link bandwidth. This does not change my recommendation. Try to limit all comms between the Robot and DS to 5MB/s max to ensure smooth operations.

FIRST also released a FMS light program so teams can practice at home, with a similar FMS in the loop. However, FMS Lite is not FMS and there is no guarantee that your performance during tests will be mirrored during a competition. [FMS Lite](http://www.usfirst.org/roboticsprograms/frc/blog-2014-fms-lite-available)

---

##When practicing at home, how can I run multiple robots with roboRio's installed?

You can do this in one of many ways. Two popular methods are below:

##Method 1

1. Use the roboRio Image tool, to image each roboRio with a different team number. (For example we would flash Robot A with 2168, and Robot B with 2169 (or any other team number that is not yours). This allows us to drive both robots simultaneously once the DS for each robot is set to the proper team number.)
2. Use the FRC Bridge Configuration Tool to configure each D-link to the respective team number of the RoboRio it is connected too.
3. Connect each Driverstation to the appropriate robot and set the team number accordingly.


##Method 2

1. Flash all roboRio's with your Team Number. (All robots's will be flashed with the same team number)
2. Manually configure the D-Link AP on each robot to broadcast a different SSID. i.e Robot2168-practice1, Robot2168-practice2
3. Connect each driver station to the corresponding Access Point for your Robot.
4. Set the team number in the DS to your team number in Each DS.

---

##How do I configure my D-link for home use?

As in previous years you can configure it automatically using the FIRST provided Bridge Configuration Tool, or you can manually configure it on your own.

###Automatic Configuration

See official documentation [ScreenSteps Live Bridge Configuration]()
You can use the FIRST provided bridge configuration tool installed on your Windows machine when you install the official FIRST utilities software.

Afterwhich place the D-Link in AP mode and connect your DS to it wirelessly.

Over the years we have adopted a practice from more experienced teams. We always leave our D-link in bridged mode, and connect it to a secondary Wireless Access point which acts as a medium between our DS and the Robot Radio. This more realistically mimicks the field setup. We also enable encrption on the D-link so to ensure all packets are encrypted just like they are on the field.

---

##Which Mode do I set my D-Link Radio (AP 2.4GHz, AP5GHz, Bridge)

At FRC Competitions, your D-Link must be in bridge mode, you can communicate with the Robot Using the USB Tether, or Ethernet Tether

At home, you can use your choice of either AP2.4 GHZ, or AP5 GHz, depending on your wireless needs.

