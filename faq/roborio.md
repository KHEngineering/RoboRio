---
layout: page
title: RoboRio FAQ
permalink: /faq/roborio/
---

<img src = "../../Images/roborio.jpg">

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

##What If I accidently plug into 24V power?
The new RoboRio will not be damaged. It will sense any voltage over 16V and safely shut down the systems which can not handle the voltage. You will need to remove the 24VDC supply and provide a suitable input voltage before the RoboRio can start up again.

---

##Can I program over USB, Ethernet, and WIFI?
For all languages deploying code using previous cRIO methods still work. That is programming via Ethernet Tether or wireless using a (D-link in AP mode) are all supported.

The RoboRio offers the addition to program over the USB host port. The drivers for the RoboRio emulate a Ethernet Controller when plugged in via USB. This USB Ethernet port is always static, and can be used to program or modify the roborio. It put the RIo on the network 172.22.11.2. Since the Rio uses mDNS, you can use your driverstation via USB, without changing any Ethernet settings. We still set our IP to a static IP on the RoboRio and Driverstation.

The USB drivers are installed on the computer when the FRC Utilities are installed which is provided in the official software released by NI.

---

##How do I set my team number and IP?

You no longer need to set the IP address for the RoboRio. The new 2015 System uses mDNS and dynamic addressing to find all devices. Static IP addresses are no longer needed. To learn more about mDNS as it applies to FRC see the [FMS FAQ](/RoboRio/faq/fms/)

Your team number will be assigned to the RoboRio when you image the Rio for the first time. After which you can access the RoboRio using RoboRio-2168.local (replacing 2168 with your own 4 digit team number, prefix 0 for 3 digit teams). 

For those teams wishing to assign their own static IP to the RoboRio you can still do this through the web interface. Once the RoboRio has been successfully images, navigate to http://RoboRio-2168.local, and check your network settings. You can login as admin and change the ethernet port from dhcp to static and assign your own 10.TE.AM.2 address.
You can always check all of your network interface settings, and modify them through the web interface of the Rio. You must be logged in as `admin` to make any changes. 

---

##How do I access the RoboRio WebServer?

Simply navigate to any of the RoboRios IP address from any computer on the same network. 
i.e http://RoboRio-2168.local (replace 2168 with your team number) over Ethernet using mDNS, http://10.TE.AM.2 if you assigned a static IP or http://172.22.11.2 when using the USB cable.

If this is your first time starting up the RoboRio, the Ethernet port is set to DHCP, and the USB
port is configured to static IP 172.22.11.2 address when connected to a computer that has the USB Driver installed (supplied when FRC Utilities are installed).

Once you determine the IP address of the RoboRio, make sure your network interface card is also on the same network as the RoboRio, and you can navigate to the RoboRio in any browser which supports the Microsoft silverlight plugin to view the RoboRio webpage.

> Note: Fellow linux users, silverlight doesn't mesh well with *nix system. If you are on a linux machine you can try to install moonlight (which is a port of silverlight, unfortunately NI has no alternatives to access the WEB site other than through the silverlight plug-in at this time)

Click the login button in the top right corner and login with the `admin` user.


---



##How do I access the Linux Operating System on the RoboRio?

The RoboRio is a headless device, meaning it is designed to run without using a display. If you would like to access the underlying linux filesystem you will need to use another device to do so.
You can access the linux operating system in any of 3 ways:

1. Use a shell terminal through SSH
2. Use SFTP through a client like filezilla
3. Use FTP through a client like filezilla

The method you choose is largely based on what operation you are trying to berform.

Using another computer you can use the secure shell protocol to access the RoboRio. You will need to connect to the RoboRio via ethernet tether, WIFI, USB and know the IP address of the RoboRio or use RS-232 with Console out enabled (for shell terminal only).


###Shell Terminal

From Linux or Mac: Open Terminal and type `ssh -l admin <IP of RoboRio>`
From Windows install [putty](http://www.putty.org) and configure it to SSH to the roborio ip address.

When asked for a password leave it blank and hit `enter`

Using SSH, you will have terminal access to the RoboRio Linux filesystem and can run linux based commands, create/delete files or folders etc and execute programs.

###SFTP
1. Add a SFTP client to your web browswer. [Filezilla client](https://filezilla-project.org/) is freeware
2. Configure it to connect to the IP address of the RoboRio
3. Login using the 'admin' user
4. You will see a folder structure of the RoboRio which will allow you to navigate its file system

You can use this method to browse the file system on the Rio, transfer files to/from RoboRio, read files, create/delete  files or folders


###FTP
It is possible to use the FTP protocol on the Rio, however only anonymous login is supported by default. The problem with that is when transfering or creating files via FTP, the file permissions are not set properly so use shell or SFTP and avoid using FTP on the Rio.

---

##What user name should I use to have root access to the file system?

The Login information for the RoboRio from the factory is:

```
username: admin
password: <leave blank> there is no password
```

You can use this login via ssh or on the RoboRio webserver page to make configuration changes.

---

##Why are the IO pins spaced so far apart, I like the way it was on the old DSC?
Well, in all honesty I don't know. But I would speculate it is to make it a lot easier for teams to plug/un-plug 3-pin header connectors. Especially rookies. With the old DSC you could plug in a connector in pin 10, but acutally think you were plugged in pin 9 because of how close the pins were, and causing a debugging mess. The space avoids this debackle.

The pins are spaced by 2 0.1" headers. A 4 pin header can be used to bridge the gap, if a team desires to use two signal pins on 1 connector (for a quadrature encoder for example)

<img src="../../Images/dualpin.png">


---

##What do the LEDs on the Rio mean?

* Power
  - Green = Rio input voltage is acceptable
  - Orange = Rio input voltage is unacceptable
  - Off = Rio is not powered on

* Status
   - Normal Operation:
       - Solid Green = Robot in Teleop Mode
       - Solid Yellow = Robot in Auto Mode
       - Solid Red = Robot in Test Mode
       - Off = Rio booted-up correctly, Robot in Disabled Mode
    
    - Error Mode
       - 2 Blinks Repeatedly = Error Detected in Software, RoboRio is put into Safe Mode Automatically, Re-image RoboRio using Imaging Tool
       - 3 Blinks Repeatedly = User Directed RoboRio to start in Safemode, Recycle Power to exit safemode and boot normally
       - 4 Blinks Repeatedly = Software Crashed Multiple times, Most likely running out of Memory during program run
       - Continuous Blinking  = Catastrophic Unrecoverable Error, FileSystem is corrupt, use Seial to Debug and Contact NI
            

* COMM = green means robot code.  Red means comms with DS, but no robot code.

* RSL = solid means powered.  Blinking means enabled.

---

##How do I upgrade the Image or Install new Firmware?
So far for Beta testing the RoboRio software has been delivered in two parts, a Firmware, and an Image. The Firmware is for the FPGA, and the Image is to load the operating system, linux file system and default settings.

The user can upgrade the firmware over Ethernet Tether/WIFI or USB. USB method is preferred and you should use that when ever possible, although we have had no problems updating the system over Ethernet/Wifi. 

The Image and Firmware will be provided via an FRC Tools Software installation by FIRST/NI. This must be installed on a Windows 7/8 computer running 32 or 64 bits.

###Firmware Upgrade: 
   1. Connect to the RoboRio via USB
   2. login to the RoboRio webpage using your internet browser (You will need to have silverlight plugin). (Labview teams can use webpage of NI Max, Java/C++ teams must use WebPage).
   3. http://10.xx.xx.2 when using ethernet or http://172.22.11.2 when using USB. Login using "admin" as the user name and leave the password field empty. Click on the RoboRio icon and select upgrade firmware. 
   4. Browse to the firmware you wish to use and apply (Typically in c:/program files(x86)/national instruments/shared/firmware/FXXX/
   5. The RoboRio will update the firmware, and if successful the new firmware version will be showed on the webpage. If not, just try again.

###Image Upgrade:
   1. Connect to the RoboRio via USB and Power on the RoboRio
   2. Open the RoboRio Imagine tool installed when the NI tools were installed (Typically in c:/program files(x86/national instruments/Labview 2014/projects/RoboRio Imaging Tool/
   3. Once Open select scan to find the RoboRio connected
   4. Enter your team number, select format controller, and select the image you wish to use. click on Format
   5. Formatting will take a few minutes, and once complete the program will notify you.
   6. The new image version will show on the Image Tool
   7. Verify the RoboRio Power is Green and Status light is off (that means all went well).
   8. Java Teams Only (Reload the Java 8 Virtual Machine (JVM) on RoboRio)
   9. All Teams - Upload Code to the RoboRio

---

##I did something to the RoboRio, and now I can not communicate with it at All. HELP? Is it Bricked?
No. Its nearly impossible to brick this thing. Follow these steps to regain communication.

When we tried to image the RoboRio prior to installing a compatible firmware we noticed this caused a state where we lost complete communication with the Rio. Upon start up, the power light was green and the status led was solid for the first 3 seconds and then flashed about 2 times a second for the remainder of the time. Power cycling or hitting the reset button alone during this time, did not change the outcome. The Rio would start up and the status led would start to blink at this constant rate.

During this time, all power to the peripherals seems to have been off. The USB port and Ethernet ports didn't seem to be powered anymore so the Imaging tool could not find the device and the ethernet link was down. We were unable to establish any link or comms to the RoboRio.

If you experience the above symptoms, hold down the reset button for 10 seconds, I held it down for about 30 seconds and after release the RoboRio should start back up. This puts the RoboRio in safemode and loads a default/clean filesystem from the factory.  The Status LED should change. We noticed it started to pulse, about 3 blinks then pause, then 3 blinks and pause, and continue this way.

After putting the Rio in safemode, I notice all the peripheral ports were back up and we were able to http back into the RIO using the initial static IP setup. 10.TE.AM.2. The status of the RIO was SafeMode, no software, as shown by the webserver. If you did not have a static IP set, you can use the USB port to have ethernet access to the RoboRio.

You can now login to the RoboRio webpage, and update the firmware. Once I updated the firmware through the Web interface, the RIO was back to normal operations.

You can then re-image the RoboRio using the RoboRio Imaginge tool and ensue normal operations. 
 
--- 

##What is CAN?
CAN is a 2 wire serial bus mostly used in cars. Its an interface with a specific protocol just like I2C or RS-232. We can use it in robotics to communicate with multiple CAN devices such as the pneumatics control module, the power distribution board, and different motor controllers such as the Jaguar and CAN Talons. The CAN bus needs to be terminated by resistors at each end to prevent reflections. The RoboRio has a built in hardwired terminal resistor so it should always be placed at the beginning of the bus. The 2015 Power distribution panel has a jumper selectable terminal resistor, so you can place the PDP at the end of the bus, and have any number of CAN devices between the RoboRio and the PDP board. The CAN interface is a differential signal, so be sure to use a twisted pair wire to prevent against EMI.

---

##How do I connect to the Internet using the RoboRio
Assuming you are connected to a network that has an internet connection, you need to set the default gateway and DNS server on the RoboRio. Use your browser to connect to the RoboRio webserver and click on login using `admin` as the user name, and leave the password blank. Select the Network interfaces Icon, and under eth0 select `advanced` to modify the default gateway and provide a DNS server. Here is a pic of what our setting look like:

<img src="../../Images/internetsettings.png">

---

##Can I install 3rd party packages/software on the RoboRio?
Yes, the roboRio uses OPKG package manager. You can run OPKG from the terminal and install packages that way. There is a public repository for the RoboRio released by NI here:XXXXXXXXXXXXX

The RoboRio is an ARM processor based on soft VFP registers with NEON instruction support. You can use any binary that has been compiled for ArmV7 with softFP on the RoboRio.

Luckily, you can make use of the Angstrom Repository to load additional software onto the RoboRio. To add the Angstrom Repo to the RoboRio package manager, follow the steps below:

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
14. use `opkg search <package> to see what you can install from the Angstrom repo onto the RoboRio.  

---

##Can I use 3.3V sensors on the RoboRio?
In short - yes. The power output pins on the RoboRio DIO pins and Analog pins are all 5V outputs by default. There is a jumper to set the DIO pins to 3.3V output but is internal to the Rio and you must remove the case to do so. This is not something FIRST or NI envisons teams to do frequently. I would suggest stick with one voltage source for all sensors, or use external supplies instead of going into the RoboRio.
The jumper is located inside the RoboRio case next to the connector for DIO9. See attached photo for details. When no jumper is installed the voltage output is 0V.
 
The jumper only affects the DIO power pins on the built-in DIO connectors, it does not affect the analog power output, or any power output pins in the MXP port. The MXP has both power supply rails included, so you can use either 5V or 3.3V supplies from the MPX without changing the internal jumper.
All DIO signal pins are 3.3 V drive and 5 V tolerant, so if you power your 3.3V sensor from an external source, the signal will be interpreted correctly on the IO pin without any jumper change.
 
---

##How do I drive 6V servos on the RoboRio?
Just plug it into any PWM port. All PWM outputs on the RoboRio are 6V output power (center pin), 5v signals (signal pin). There is no jumper cable to modify the output voltage (center pin or signal pin) of the PWM rail. All motor controllers for FRC have the center pin on the PWM disconnected (so they don't use the 6V pin), they only use ground and signal. Therefore, the 6V output is always present, and used to drive a servo if a servo is connected to any PWM pin. 

---

##What happens when the RoboRio voltage drops?
As the input voltage drops below a specifed voltage, certain systems are turned off automatically. The brownout condition I believe starts when the input voltage to the RoboRio dips below 6.8V, at the moment it is unclear if it needs to stay below this level for any period of time.

The PDP Power supply to the RoboRio is not regulated, the RoboRio regulates its own power internally. This was a concious decision made by the design team.

Here is the breakdown of the logic we noticed during brownout testing:

input voltage is 7.5V and above
    All RoboRio Systems are fully functional, Power LED is Green
input voltage Below 6.8V, Power LED is Organge
	RoboRio Power light goes from Green to Red
	All PWM Output signals are disabled (Motor controllers are neutral)
	6V Servo Output power is disabled
input voltage power Below 6.3V
    All DIO 5V output power is disabled (RoboRio and MXP)
    All 3.3V output is disabled (RoboRio and MXP)
    Digital Input and Analong input signal pins are still active
input voltage Below 4.0V, Power LED is Off
    RoboRio Processor died
    No longer able to read an DIO channel states
    Loss of Comms with Robot


From my understanding, the regualtor topology on the RoboRio is such that the 6V supply feeds the 5V supply, and the 5V supply feeds the 3,3V supply. So upon a brownout event, (VbattIn < 6.8 V) PWM output and 6V servo power are deactivated, but the 6V supply is still operational (so 5V and 3.3V rails are still operational). When the RoboRio drops below 6.3V, the 6V regulator can no longer be sustained so the 6V, 5V and 3.3V power are lost. 

This means there is now ~ 0.6 V between when the motors are disabled and when the 5 V and 3.3 V supplies shut down instead of them happening at the same time.

I believe there is current work on a feature that will allow the FPGA to stop motor controllers (probable source of brown-out in non-pathological case) in far less time. The plan is to actively send one PWM pulse of "idle" when commanded to disable by the watchdog / power monitor before stopping the generation of PWM signals. Because the motor controllers are not continuing to draw high current for as long, the voltage drop should be less severe. This should reduce the time from brown-out detection to load removal from 100 ms +/- 5ms to about 10 ms +/- 5 ms.

Here is a pic of the Regulator Topology:

<img src="../../Images/regulatortopology.png">

---

##Will we lose encoder counts while that happens (encoder brownout)?

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

 
 The bus switch that adjusts the signals passed to the FPGA is powered by a supply that is sourced by the buck-boost that powers the controller as a whole. That supply operates down to 4.5 V. That means that if you decide to power your encoder with a supply other than the one provided and the provided supply browns out, the signals will still make their way to the FPGA. As noted earlier, if your sensor depends on pull-up resistors (like limit switches or banner sensors or open-collector output encoders) then you will also need to add pull resistors connected to your external supply. You should be able to test this by either using the new power API to disable the 5 V supply manually or by installing a jumper between 5 V and Ground which puts the supply in protection.
 
---

##What are some of the linux based information I should know?

Kernel: 
File System: UBI
Boot Loader: uboot
Init: SystemV

---

##How do I put the RoboRio in Safe Mode?

Hold the Reset Button for 5 seconds and release, The RoboRio will rebot and the status light will blink 3 times repeatedly. This indicates the RoboRio is now in Safe Mode

To get out of Safemode reboot the RoboRio by pressing the Reset Button, issuing a `reboot` Command in the terminal, or power cycle.

---

##How to I commuicate with the RoboRio over Serial (RS-232)

The Serial Information is:
– 115,200 bits per second
– Eight data bits
– No parity
– One stop bit
– No flow control

You will need to buy USB-to-serial adapter and make a DB-9 to 3-pin header cable. Follow Instructions here: []()



On Linux:
	1. Install minicom `sudo apt-get install minicom`
	2. plug in the USB-to-serial converter and wait a couple of seconds
	3. Find out which port the adapter is assigned `dmesg | grep tty` (output should be something like ttyUSB0)
	4. Open second terminal window
	5. Configure MiniCom with the above settings `sudo minicom -s`
	6. Exit Minicom, the modem should initialize, hit enter and the terminal should now show the RoboRio terminal (assuming the cable is correct) 

On Windows:

---

##What is the MXP port?

The Modular Expansion Port (MXP) is an additional breakout that provides access to all the dedicated ports on the RoboRio and includes additional shared PWM pins/DIO pins/Analong Pins and serial interfaces.
The MXP also has 5V and 3.3V sources. You can use this port to make your own custom board or buy pre-made boards.

[Make your Own Board FIRST Compliance](http://www.usfirst.org/roboticsprograms/frc/blog-myrio-expansion-port-whats-the-deal)
[Pre-made board from Rev Robotics](http://www.andymark.com/product-p/am-2995.htm) 

---

##What does a shared PIN on the MXP mean?

A "shared" pin means that the pin can be in a multitude of ways, and you can choose which way to use that pin in your robot program.

For example shared PWM pins on the MXP means you can either use that pin to provide a PWM signal (for a motor controller) or you can use it as a Digital Input Signal, or as a Digital Output Signal.
 
