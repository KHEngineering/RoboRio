---
layout: page
title: RoboRio FAQ
permalink: /roborio/
---

##Specs: 

Dual-Core Arm Coretex A9 @ 667 MHz
256MB RAM for System Memory
256 MB NAND for NonVolitile Memory
Runs Linux Kernel patched with pre_emtRT
Input Power: 6.8 to 16V (brownout from 4.5 to 6.8VDC)

PWM:20 (10 dedicated on PWM Rail, 10 shared on MXP)
DIO:26 (10 dedicated on DIO Rail, 16 shared on MXP)
Relay:4 Dual-output channels (FWD/REV)

---

##What If I accidently plug into 24V?
The new RoboRio will not be damaged. It will sense any voltage over 16V and safely shut down the systems which can not handle the voltage

---

##Can I program over USB, Ethernet, and WIFI?
For all languages deploying code using previous cRIO methods still work. That is programming via Ethernet Tether or wireless using a (D-link in AP mode).
The RoboRio offers the addition to program over the USB host port. The drivers for the RoboRio emulate a Ethernet Controller when pluged in via USB. This USB Ethernet port is always static, and can be used to program or modify the roborio. It put the RIo on the network 172.22.11.2. Since the Rio uses mDNS, you can use your driverstation via USB, without chaning any Ethernet settings.

---

##How do I set my team number?
Your team number IP address will be set when you image the Rio for the first time. However, you can always check all of your network interface settings, and modify them through the web interface of the Rio. Simply navigate to any of the RoboRios IP address from any computer on the same network. 
i.e http://10.xx.xx.2 over ethernet, or http://172.22.11.2 when using the USB cable.

---

##Why are the IO pins spaced so far apart, I like the way it was on the old DSC?
Well, in all honesty I don't know. But I would speculate it is to make it a lot easier for teams to plug/un-plug 3-pin header connectors in. Especially rookies. With the old DSC you could plug in a connector in pin 10, but acutally think you were plugged in pin 9 because of how close the pins were, and causing a debugging mess. The space avoids this debackle.

---

##What do the LEDs on the Rio mean?
Status = Green for Teleop, yellow for auto, Red for test mode, off for disabled

COMM = green means robot code.  Red means comms with DS, but no robot code.

RSL = solid means powered.  Blinking means enabled.

---

##How do I upgrade the Image or Install new Firmware?
So far for Beta testing the RoboRio System has been delivered in two parts, a Firmware, and an Image. The Firmware is for the FPGA, and the Image is to load the operating system and default settings.
The user can upgrade the firmware of Ethernet/WIFI or USB. Although the USB method is preferred. To upgrade the firmware login to the RoboRio webpage using your internet browser (You will need to have silverlight plugin). 
httP://10.xx.xx.2 when using ethernet or http://172.22.11.2 when using USB. Login using "admin" as the user name and leave the password field empty. Click on the RoboRio icon and select upgrade firmware. 

---

##I Imaged the RoboRio before Flashing it, and now I can not communicate with it. HELP? Is it Bricked?
No. Its nearly impossible to brick this thing. Follow these steps to regain communication.

This caused a state where we lost complete communication with the Rio. Upon start up, the power light was green and the 
status led was solid for the first 3 seconds and then flashed about 2 times a second for the remainder of the time. 
Power cycling or hitting the reset button alone during this time, did not change the outcome. The Rio would start up and
 the status led would start to blink at this constant rate.

During this time, all power to the peripherals seems to have been off. The USB port and Ethernet ports didn't seem to be
 powered anymore so the Imaging tool could not find the device and the ethernet link was down. We were unable to 
establish any link or comms to the rio.

Right before I was going to try and connect through serial using hyper terminal, I had the idea to just hold down both 
the reset and user buttons. I held them down for about 30 seconds and after I released them, the roboRio started back up
, but the Status LED changed, it started to pulse, about 3 blinks then pause, then 3 blinks and pause, and continue this
 way.

However, I did notice, all the peripheral ports were back up and we were able to http back into the RIO using the 
initial static IP setup. 10.TE.AM.2. The status of the RIO was SafeMode, no software.

The software image was V2 however, with the old firmware.

Once I updated the firmware through the Web interface, the RIO was back to normal operations.

My question is what really happened here. Was the Rio in some sort of crashed state, and did a limited power up? What 
function does holding down both buttons do, is that a soft or hard reset, or just enters safe mode?. I was curious to 
know what output I would have seen over the serial port. Would I have been able to TFTP into the device?

I am never too worried about bricking the Rio's, there always seems to be some way back in to establish comms and get it
 back up and running.
 
--- 

##What is CAN?
CAN is a 2 wire serial bus mostly used in cars. Its an interface with a specific protocol just like I2C or RS-232. We can use it in robotics to communicate with multiple CAN devices such as the pneumatics control module, the power distribution board, and different motor controllers such as the Jaguar and CAN Talons. The CAN bus needs to be terminated by resistors at each end to prevent reflections. The RoboRio has a built in hardwired terminal resistor so it should always be placed at the beginning of the bus. The 2015 Power distribution board has a jumper selectable terminal resistor, so you can place the PDP at the end of the bus, and have any number of CAN devices between the RoboRio and the PDP board. The CAN interface is a differential signal, so be sure to use a twisted pair wire to prevent against EMI.

---

##Can I install 3rd party packages/software on the RoboRio?
Yes, the roboRio uses OPKG package manager. You can run OPKG from the terminal and install packages that way. There is a public repository for the RoboRio released by NI here:XXXXXXXXXXXXX

---

##Can I use 3.3V sensors on the RoboRio?
The RoboRio DIO pins and Analog pins are all 5V by default. There is a jumper to set them to 3.3V but is internal to the Rio and you must remove the case to do so. This is not something FIRST or NI envisons teams to do frequently. I would suggest stick with one voltage source for all sensors, or use external supplies instead of going into the RoboRio.
The voltage for the digital i/o connectors is jumper selectable for either 3.3V or 5V. The jumper is located next to the
connector for DIO9. See attached photo for details. When no jumper is installed the voltage is 0V.
 
The jumper only affects the DIO power pins on the built-in DIO connectors. The MXP has both power supply rails included, so the board may use either one as needed. The I/O itself in both MXP and built-in DIO is not affected by the jumper. All DIO is 3.3 V drive and 5 V tolerant.
 
---

##My big question is whether or not we will lose encoder counts while that happens (encoder brownout). The digital side car would brown the encoders out below 5.5 volts, which caused us to destroy a gear once. We'll have to add that to our list of things to test.
Unfortunately the topology of the power supplies that feed external user devices like the encoders is part of the system that does not "survive". Based on alpha team feedback, we are making some small adjustments to make it last longer, but the topology doesn't help with that case. The structure looks like this:



Code:
VbattIn ----[6 V "servo" supply]-----[current limit/disable]---6 V terminals
                                    \
                                     ----[5 V user supply]-----5 V terminals
                                      \
                                       --[3.3 V user supply]---3.3 V terminals
The change we made was to not disable the 3.3 V or 5 V supplies when we detect a brown-out condition (VbattIn < 6.8 V). This helps a bit for the 5 V to survive, but when the VbattIn drops to about 6.2 V, the 6 V servo supply is no longer able to stay active, so the 5 V and 3.3 V supplies drop out with a source voltage fault.

 It does mean there is now ~ 0.6 V between when the motors are disabled and when the 5 V and 3.3 V supplies shut down instead of them happening at the same time.

 I'm also working on a feature that will allow the FPGA to stop motor controllers (probable source of brown-out in non-pathological case) in far less time. The plan is to actively send one PWM pulse of "idle" when commanded to disable by the watchdog / power monitor before stopping the generation of PWM signals. Because the motor controllers are not continuing to draw high current for as long, the voltage drop should be less severe. This should reduce the time from brown-out detection to load removal from 100 ms +/- 5ms to about 10 ms +/- 5 ms.


##Explainations

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
 