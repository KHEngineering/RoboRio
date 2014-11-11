---
layout: page
title: RoboRio FAQ
permalink: /faq/roborio/
---

<img src = "http://khengineering.github.io/RoboRio/Images/roborio.jpg">

##Specs: 

Dual-Core Arm Cortex A9 @ 667 MHz
256MB RAM for System Memory
256 MB NAND for NonVolitile Memory
Runs Linux Kernel patched with pre_emtRT
Input Power: 6.8 to 16V (brownout from 4.5 to 6.8VDC)

PWM:20 (10 dedicated on PWM Rail, 10 shared on MXP)
DIO:26 (10 dedicated on DIO Rail, 16 shared on MXP)
Relay:4 Dual-output channels (FWD/REV)
Analog: 8 Analog Inputs, 0v-5V, 12-bit 500 thousand samples per second
Analog: 2 Analog Outputs, 0v-5V, 12-bit 340 thousand samples per seconds  
Serial: i2c, RS-232, TTL, SPI
USB 2.0

---

##What If I accidently plug into 24V?
The new RoboRio will not be damaged. It will sense any voltage over 16V and safely shut down the systems which can not handle the voltage. You will need to remove the 24VDC supply and provide a suitable input voltage before the RoboRio can start up again.

---

##Can I program over USB, Ethernet, and WIFI?
For all languages deploying code using previous cRIO methods still work. That is programming via Ethernet Tether or wireless using a (D-link in AP mode) are all supported.

The RoboRio offers the addition to program over the USB host port. The drivers for the RoboRio emulate a Ethernet Controller when plugged in via USB. This USB Ethernet port is always static, and can be used to program or modify the roborio. It put the RIo on the network 172.22.11.2. Since the Rio uses mDNS, you can use your driverstation via USB, without changing any Ethernet settings. We still set our IP to a static IP on the RoboRio and Driverstation.

The USB drivers are installed on the computer when the NI MAX software is installed which is provided in the official software released by NI.

---

##How do I access the RoboRio WebServer settings?

Simply navigate to any of the RoboRios IP address from any computer on the same network. 
i.e http://10.xx.xx.2 over ethernet, or http://172.22.11.2 when using the USB cable.

If this is your first time starting up the RoboRio, the Ethernet port is set to DHCP, and the USB
port is configured to static IP 172.22.11.2 address when connected to a computer that has the USB Driver installed (supplied when NI MAX is installed).

Once you determine the IP address of the RoboRio, make sure your network interface card is also on the same network as the RoboRio, and you can navigate to it in any brower, which supports the Microsoft silverlight plugin to view the RoboRio webpage.

> Note: Fellow linux users, silverlight doesn't mesh well with *nix system. If you are on a linux machine you can try to install moonlight (which is a port of silverlight, unfortunately NI has no alternatives to access the WEB site other than through the silverlight plug-in at this time)

Click the login button in the top righr corner and login with:
```
username: admin
password: <leave blank> there is no password
```

---

##How do I set my team number?
Your team number IP address will be set when you image the Rio for the first time. However, you can always check all of your network interface settings, and modify them through the web interface of the Rio. 

---

##How do I connect to the Internet using the RoboRio
Assuming you are connected to a network that has an internet connection, you need to set the default gateway and DNS server on the RoboRio. Use your browser to connect to the RoboRio webserver and click on login using `admin` as the user name, and leave the password blank. Select the Network interfaces Icon, and under eth0 select `advanced` to modify the default gateway and provide a DNS server. Here is a pic of what our setting look like:

<img src="http://khengineering.github.io/RoboRio/Images/internetsettings.png">


---

##How do I access the Linux Operating System on the RoboRio?

The RoboRio is a headless device, meaning it is designed to run without using a display. If you would like to access the underlying linux filesystem you will need to use another device to do so.

Using another computer you can use the secure shell protocol to access the RoboRio. You will need to connect to the RoboRio via ethernet tether, WIFI, or USB and know the IP address of the RoboRio.

From Linux or Mac: Open Terminal and type `ssh -l admin <IP of RoboRio>
From Windows install [putty](http://www.putty.org) and configure it to SSH to the roborio.

The Login information for the RoboRio from the factory is:
```
username: admin
password: <leave blank> there is no password
```

Using SSH, you will hever terminal access to the RoboRio Linux filesystem

---

##Why are the IO pins spaced so far apart, I like the way it was on the old DSC?
Well, in all honesty I don't know. But I would speculate it is to make it a lot easier for teams to plug/un-plug 3-pin header connectors. Especially rookies. With the old DSC you could plug in a connector in pin 10, but acutally think you were plugged in pin 9 because of how close the pins were, and causing a debugging mess. The space avoids this debackle.

The pins are spaced by 2 0.1" headers. A 4 pin header can be used to bridge the gap, if a team desires to use two signal pins on 1 connector (for a quadrature encoder for example)

<img src="http://khengineering.github.io/RoboRio/Images/dualpin.png">


---

##What do the LEDs on the Rio mean?
Status = Green for Teleop, yellow for auto, Red for test mode, off for disabled

COMM = green means robot code.  Red means comms with DS, but no robot code.

RSL = solid means powered.  Blinking means enabled.

---

##How do I upgrade the Image or Install new Firmware?
So far for Beta testing the RoboRio software has been delivered in two parts, a Firmware, and an Image. The Firmware is for the FPGA, and the Image is to load the operating system and default settings.
The user can upgrade the firmware over Ethernet Tether/WIFI or USB, Although the USB method is preferred, we have had no problems updating the system over Wifi. To upgrade the firmware login to the RoboRio webpage using your internet browser (You will need to have silverlight plugin). 
httP://10.xx.xx.2 when using ethernet or http://172.22.11.2 when using USB. Login using "admin" as the user name and leave the password field empty. Click on the RoboRio icon and select upgrade firmware. 

Browse to the location of the firmware you wish to use, and apply. The RoboRio will update the firmware, and if successful the new firmware version will be showed on the webpage. If not, just try again.

Once the firmware is updates, you can use the RoboRio Imaging tool (installed when the NI software is installed) to update the image. Open the tool, enter your team number, select "format controller" and select "ok". This will image the RoboRio. Confirm that your network settings are still correct after the image, and your done.

Note: Each Image is only compatible with a certain firmware. If you are trying to load an image on an incompatible firmware, we noticed that this will just cause the RoboRio to crash. If this happens, you can recover the RoboRio by following the steps in the next question.  

---

##I Imaged the RoboRio before Flashing it, and now I can not communicate with it. HELP? Is it Bricked?
No. Its nearly impossible to brick this thing. Follow these steps to regain communication.

When we tried to image the RoboRio prior to installing a compatible firmware we noticed his caused a state where we lost complete communication with the Rio. Upon start up, the power light was green and the status led was solid for the first 3 seconds and then flashed about 2 times a second for the remainder of the time. Power cycling or hitting the reset button alone during this time, did not change the outcome. The Rio would start up and the status led would start to blink at this constant rate.

During this time, all power to the peripherals seems to have been off. The USB port and Ethernet ports didn't seem to be
 powered anymore so the Imaging tool could not find the device and the ethernet link was down. We were unable to 
establish any link or comms to the rio.

If you experience the above symptoms, hold down the reset button for 10 seconds, I held it down for about 30 seconds and after release the RoboRio should start back up. This puts the RoboRio in safemode and loads a default/clean filesystem from the factory.  The Status LED schanged. We noticed it started to pulse, about 3 blinks then pause, then 3 blinks and pause, and continue this way.

However, I did notice, all the peripheral ports were back up and we were able to http back into the RIO using the 
initial static IP setup. 10.TE.AM.2. The status of the RIO was SafeMode, no software. If you did not have a static IP set, you can use the USB port to have ethernet access to the RoboRio.

You can now login to the RoboRio webpage, and update the firmware. Once I updated the firmware through the Web interface, the RIO was back to normal operations.

You can then re-image the RoboRio and ensue normal operations. 
 
--- 

##What is CAN?
CAN is a 2 wire serial bus mostly used in cars. Its an interface with a specific protocol just like I2C or RS-232. We can use it in robotics to communicate with multiple CAN devices such as the pneumatics control module, the power distribution board, and different motor controllers such as the Jaguar and CAN Talons. The CAN bus needs to be terminated by resistors at each end to prevent reflections. The RoboRio has a built in hardwired terminal resistor so it should always be placed at the beginning of the bus. The 2015 Power distribution panel has a jumper selectable terminal resistor, so you can place the PDP at the end of the bus, and have any number of CAN devices between the RoboRio and the PDP board. The CAN interface is a differential signal, so be sure to use a twisted pair wire to prevent against EMI.

---

##How do I connect the RoboRio to the Internet


---

##Can I install 3rd party packages/software on the RoboRio?
Yes, the roboRio uses OPKG package manager. You can run OPKG from the terminal and install packages that way. There is a public repository for the RoboRio released by NI here:XXXXXXXXXXXXX

The RoboRio is an ARM processor based device, and you can make use of the Angstrom Repository to load additional software onto the RoboRio. To add the Angstrom Repo to the RoboRio package manager, follow the steps below:

1. SSH into the RoboRio using putty on windows or terminal on any Mac or other linux based computer
2. Login using `admin` as the username and leave the password blank (just hit enter)
3. Use VI to create a new feed source for opkg `vi /etc/opkg/armstrong-base-feed.conf`
4. Hit the `i` button on your keyboard to enter insert mode in vi
5. Paste this line into the file `src/gz angstrom-base http://feeds.angstrom-distribution.org/feeds/next/ipk/eglibc/armv7a/base/`
6. Hit the `esc` button on your keyboard to exit insert mode in vi
7. Type `:wq` to save the file and exit VI
8. You should now be back at the terminal prompt $, type `reboot` to restart the roborio (You will loose SSH connection)
9. Once the RoboRio restarts reconnect to it via SSH (same procedure as above) and once at the prompt type `opkg update`
10. If connected to the internet, your RoboRio will now download the list of angstrom packages you can safely install on your RoboRio.
11. use `opkg install <package>` to install new software on the RoboRio
12. use `opkg updgrade <package>` to upgrade packages
13. use `opkg list-installed` to see what you already have installed on the RoboRio  

---

##Can I use 3.3V sensors on the RoboRio?
In short - yes. The power output pins on the RoboRio DIO pins and Analog pins are all 5V outputs by default. There is a jumper to set the DIO pins to 3.3V output but is internal to the Rio and you must remove the case to do so. This is not something FIRST or NI envisons teams to do frequently. I would suggest stick with one voltage source for all sensors, or use external supplies instead of going into the RoboRio.
The jumper is located inside the RoboRio case next to the connector for DIO9. See attached photo for details. When no jumper is installed the voltage output is 0V.
 
The jumper only affects the DIO power pins on the built-in DIO connectors, it does not affect the analog power output, or any power output pins in the MXP port. The MXP has both power supply rails included, so you can use either 5V or 3.3V supplies from the MPX without changing the internal jumper.
All DIO signal pins are 3.3 V drive and 5 V tolerant, so if you power your 3.3V sensor from an external source, the signal will be interpreted correctly on the IO pin without any jumper change.
 
---

##How do I drive 6V servos on the RoboRio?
All PWM outputs on the RoboRio are 6V output power, 5v signals. There is no jumper cable to modify the output voltage of the jumper cable. All motor controllers for FRC have the center pin on the PWM disconnected (so they don't use the 6V pin), they only use ground and signal. Therefore, the 6V output is always present, and used to drive a servo is a servo is connected to any PWM pin. 


---

##What happens when the RoboRio voltage drops?
As the input voltage drops below a certain level, certain systems are turned off automatically. The brownout condition I believe starts when the input voltage to the RoboRio dips below 6.8V, at the moment it is unclear if it needs to stay below this level for any period of time.

```
VbattIn ----[6 V "servo" supply]-----[current limit/disable]---6 V terminals
                                    \
                                     ----[5 V user supply]-----5 V terminals
                                      \
                                       --[3.3 V user supply]---3.3 V terminals
```

The change we made was to not disable the 3.3 V or 5 V supplies when we detect a brown-out condition (VbattIn < 6.8 V). This helps a bit for the 5 V to survive, but when the VbattIn drops to about 6.2 V, the 6 V servo supply is no longer able to stay active, so the 5 V and 3.3 V supplies drop out with a source voltage fault.
It does mean there is now ~ 0.6 V between when the motors are disabled and when the 5 V and 3.3 V supplies shut down instead of them happening at the same time.
I believe there is current work on a feature that will allow the FPGA to stop motor controllers (probable source of brown-out in non-pathological case) in far less time. The plan is to actively send one PWM pulse of "idle" when commanded to disable by the watchdog / power monitor before stopping the generation of PWM signals. Because the motor controllers are not continuing to draw high current for as long, the voltage drop should be less severe. This should reduce the time from brown-out detection to load removal from 100 ms +/- 5ms to about 10 ms +/- 5 ms.


---

##Will we lose encoder counts while that happens (encoder brownout).

Luckily the system is capable of managing current draw at many levels.
 1. The roboRIO monitors its input voltage level and coordinates brownout staging in order to prevent blackout of critical elements. This is the approach that is currently being tweaked.

 The general approach of the brownout behavior is to disable high draw components -- motor controllers -- in order to stabilize the voltage level and avoid reboots and further faults. As mentioned earlier, the alpha results were quite promising, but the response is being tweaked in order to maintain the supply rails to sensors -- both analog and digital.

 One aspect of this, detailed by Joe earlier, is to identify which PWM devices are motors and which are servos. The FPGA will then be able to disable motors directly instead of simply removing their signal and waiting for their micros to timeout. This quicker response has not been tested by the alpha or beta teams, but it is a ~10X improvement in timing control of the circuit driver.

 2. When a brownout does occur, the information will be accessible to robot code. If the motor controllers outputs are zeroed by the FPGA, this can cause integral windup in control loops. If those control loops are aware that their set point was not what they requested, they can adjust their integral state.

 If the brownout is more severe and the supply lines to servos and sensors is interrupted, the robot code can know that absolute position of some mechanisms may need to be recalibrated. 

 3. Motor controllers implement the set point, and as seen with the Jaguar, they can impose limits. Currently this is not a part of the plan.

 4. User code is in charge of motor controller set points. Ramping or limits are easy to implement. The Power API now gives feedback from the PD and roboRIO that should help with balancing performance and current draw. I don't personally have a PD to test, but it is hoped that external current sensors and monitoring isn't really required in order to make this approach effective and accessible to many teams.

 5. Robots sensors could be allowed to use a suppy that is not shared with servos. 

 There are probably others. I feel that the next step is to characterize the improvement that Joe has already implemented. I'm sure that will be accomplished in the beta. Probably quite soon.

 Greg McKaskle
 
 The bus switch that adjusts the signals passed to the FPGA is powered by a supply that is sourced by the buck-boost that powers the controller as a whole. That supply operates down to 4.5 V. That means that if you decide to power your encoder with a supply other than the one provided and the provided supply browns out, the signals will still make their way to the FPGA. As noted earlier, if your sensor depends on pull-up resistors (like limit switches or banner sensors or open-collector output encoders) then you will also need to add pull resistors connected to your external supply. You should be able to test this by either using the new power API to disable the 5 V supply manually or by installing a jumper between 5 V and Ground which puts the supply in protection.
 

 
