---
layout: page
title: Java Programming FAQ
permalink: /faq/java/
---


Major Changes:
RoboRio has a Java 8 SE Embedded JVM
Official Support for the Eclipse IDE
0 based port numbers

---

##Getting Started With Java Quick Guide

1. Wire Control System to approved wire diagram. See the [Electrical FAQ](/RoboRio/faq/electrical/) for more info.
2. Flash and Image RoboRio to Latest versions. See the [RoboRio FAQ](/RoboRio/faq/roborio/) for more info.
3. Install JVM on RoboRio. See question below.
4. Install 32-bit Java 8 Development Kit on Development Computer (http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) 
Note: Mac Users must install 64-bit JDK 
4. Download 32-bit Eclipse IDE for Java Development on Development Computer (install 32-bit even if you are on 64-bit OS)  [Luna](https://www.eclipse.org/downloads/packages/eclipse-ide-java-developers/lunasr1)
5. Extract eclipse to your desired location.
6. Open Eclipse and Install Official FRC plugins [plugin URL Released at KickOff] ()
7. Create New WPI LIb Java Project File->New->Other->WPI Robot Project
8. Enter Team Number and Name project, Select Either Command Based or Iterative Robot frameworks
9. Add JDK to build Path to your Robot Project
10. Deploy Code to Robot.

---

##How do I install the Java Virtual Machine on the RoboRio

Ensure RoboRio is flashed and Imaged to latest versions then continue with steps below.

[Offical screensteps directions](https://wpilib.screenstepslive.com/s/4485/m/13809/l/243933-installing-java-8-on-the-roborio-java-only)

###From Development Computer
1. Create an account on Oracles Website [oracle](https://login.oracle.com/mysso/signon.jsp)
2. Download the Java SE 8 Embedded JVM for ARMv7 Linux VFP, SoftFP ABI, Little Endian [ARM JVM](http://www.oracle.com/technetwork/java/embedded/embedded-se/downloads/javase-embedded-downloads-2209751.html)
3. Transfer and untar the JVM to the RoboRio using the project provided by FIRST in the official documentation or do it manually using the steps below:

###Deploy JRE Project
1. Follow Official directions

###Windows Host Machine Connected to RoboRio
1. Use SFTP via browser or WINSCP application to connect to RoboRio
2. Create director `JRE` in folder /usr/local/frc/ such that you now have a /usr/local/frc/JRE/ folder structure
3. transfer downloaded .tar.gz file to RoboRio folder /etc/bin/frc/JRE/
4. Use putty to connect to shell terminal on RoboRio. See the [RoboRio FAQ](/RoboRio/faq/roborio/) for more info.
5. Continue to Step 5 under Linux/Mac Host Machine

###Linux/Mac Host Machine Connected to RoboRio
1. Open terminal and connect to RoboRio via SSH. See the [RoboRio FAQ](/RoboRio/faq/roborio/) for more info.
2. On RoboRio terminal run `mkdir /usr/local/frc/JRE`
3. Open a second local terminal window
4. Using local terminal window Transfer downloaded file to to RoboRio `scp /home/user/downloads/ejdk-8u6-fcs-b23-linux-arm-vfp-sflt-12_jun_2014.tar.gz admin@172.22.11.2:/usr/local/frc/JRE
5. Go back to Roborio terminal and execute `cd /usr/local/frc/JRE`
6. If you run `ls` you should see the tar file we just transfered
7. Untar the tar file `tar -zxvf ejdk-8u6-fcs-b23-linux-arm-vfp-sflt-12_jun_2014.tar.gz`
8. Once complete, if you run `ls` you should see a folder similar too `ejdk1.8.0_06`
9. move the contents of this folder ` mv ejdk1.8.0_06/* .`
10. If you run 'ls' now you should see a bin folder and a bunch of other folders
11. Remove the tar file `rm ejdk-8u6-fcs-b23-linux-arm-vfp-sflt-12_jun_2014.tar.gz`
12. Remove the empty folder `rm -r ejdk1.8.0_06/`
13. Set permissions on java files `chmod +x /usr/local/frc/JRE/bin/*`
14. Done

---

##How Can I see live Program Output in Eclipse?

Use the RioLog Viewer.

To find the RIOLog window, in eclipse, go to Window, Show View, Other and search for RIOlog and you'll see it. Once you add it, it will stay around between eclipse restarts.

---

##Can I use an older version of Eclipse like Kelper with the plugins?
Yes, but only with a Java v7 or earlier JDK. There is a ANT build bug in older version of eclipse that is does not recognize the default ANT build version that is shipped with Kelper.

See the bug report here: [bug](https://wiki.eclipse.org/Ant/Java8)

We recommend using Eclipse Luna where ever possible, with JDK v8, but if you must use Kepler, downgrade the JVM to v7 or run the fix noted in the bug report to use JVM v8 with Eclipse Kepler. 

---

##When I deploy code, where is it saved on the RoboRio?

User programs are downloaded to /home/lvuser directory

---

##When I open eclipse I get an error stating "Unable to find JVM"

````This problem is most likely caused by not having a JVM or JDK installed on your computer. Please See step 

---

##When I Deploy My Java Program I get an "Unable to find Javac Message"

If you get a message similar to the one below:

```
   Unable to find a javac compiler;
   com.sun.tools.javac.Main is not on the classpath.
   Perhaps JAVA_HOME does not point to the JDK
```

It means you haven't set up your project build path with a Java Development Kit (JDK).

---

##When I deploy I get "Remote command failed with exit status 1" error

If you get an error similar to this after line `cmd : test -d /usr/local/frc/JRE`

<img src = "../../Images/eclipseerror/jvmmissingerror.png">

The most likely cause is your RoboRio does not have the Java JVM installed. Please be sure to follow the steps exactly above to install the JVM on the Roborio. 

If you believe you installed the JVM but are still receiving this error, please ensure that the JVM is in the right location and that that the bin file has the executable attribute set. 

1. Use find to determine where the JVM is located. Run `find / -name *javac*` in the Roborio termina. The `javac` application must be in the location `/usr/local/frc/JRE/bin`
2. Once the JVM is in the right folder location ensure the execute attribute is set `chmod +x /usr/local/frc/JRE/bin/*`

---

##Can you tell me whats new between 2014 Java and 2015 Java WPILib

Here Goes:

Changes for is version:
1. Wait on starting until DS is connected - Java only for now. C++ equivalent change coming
soon.
2. Java installed test on program startup
3. Image version check to make sure image version matches library.
4. NI Vision code integrated for C++ release, Java coming soon. There are two sample
programs for C++ that should get you started. There is a camera server built-in that will feed
images to the NI Dashboard. We will have support for the SmartDashboard soon.
5. We are now using the NetConsole protocol for sending output to the development system.
There is a new window in eclipse called RIOLog (thanks to Manuel from 1511). Pop this up after launching to see program 
output. You can also use the NetConsole utility that is supplied with the LabVIEW release.
6. Added FRCSim.
7. Methods added to check for robot status including Watchdog status, DS status, and
brownout status.
9. Added support for launching a simulation friendly SmartDashboard.
11. Restored the -ip option support for SmartDashboard
12. The release configuration is removed from the C++ template. This was an untested mode of
compiling programs and not the default. If it is desired to run with a higher compiler
optimization level, a team can do that in the project properties and verify that it is working.
13. We have (with some controversy) removed the timing option from the IterativeRobot
template. The belief is that it represents a distinctly different way of the template from operating from it's original
 intent which was to sync with the DS packet arrival (a 20ms loop). Teams wishing to run with other timing can easily 
use the SampleRobot template or make their own by subclassing RobotBase.
14. OutlineViewer is not part of the regular build and is now included in the tools directory.
15. An off-by-one error in Digital Output PWM Gen has been fixed (artf3705).
16. User APIs for the roboRIO power methods has been implemented (artf3728 and artf3537)
17. The "clean" step is being invoked before deploying java programs to get around the ant
builder issue with doing improper dependency checking. (art3766)
18. All samples now build with the appropriate C++11/14 syntax to avoid warnings (constexpr)
20. Fixed 0-based joysticks and joystick axis in simulation
21. PIDController loop timing is now done with a notifier to remove jitter in timing.
22. Check for fatal interrupt status on multiple interrupt methods to avoid hanging program
23. Talon now uses 1X update rate (artf 3733)
24. Use ByteBuffer for conversion from raw sensor byte to Java types
25. Remove unimplemented sendErrorStreamToDriverStation method
26. Detect projects which are duplicates on Windows due to casing
27. Update Interrupt Javadocs
28. DigitalInputs are now automatically added to LiveWindows in both C++ and Java
29. No longer raising exception for Joystick axis/POV out of range (Thanks to Peter Johnson) 30. 
30. User programs are now downloaded to /home/lvuser
31. Added isEnabled() method calls to loops in sample programs
32. Added a message to notify users of unsupported simulation platform. 33. Fixed issue with RobotBuilder jar files.
34. Re-added the Wiring.html file to RobotBuilder
35. using mDNS name derived from team number in SmartDashboard

Still have more to come that didn't make it in today:
- Talon SRX CAN support
- additional camera and vision support (java bindings for NIVision - thanks Peter) - a glitch filter from Austin Schuh 
on 971
- an OpenCV library build for the roboRIO complete with C++ and Java bindings. - and more smaller improvements
- Many more sample programs
- Java driver station test mode flag set correctly
- Number of joysticks increased to 6
- Additional joystick support implemented including POV
- Runtime errors are now more properly passed to the DS Log
- Jaguar getControlMode() is now public
- Relay "On" state can now be set from SmartDashboard
- Wait() now recovers from signals - continues to wait for remaining time
- Preferences class now checks for [ and ]
- Scheduler now runs in disabled mode
- Add SmartDashboard methods with default values to match network tables
- Add method to get the CAN device ID for Jaguar


SmartDashboard now uses mDNS by default. The command line argument is temporarily removed, but you can set either mDNS 
or IP address in the preferences.

- home path stored in newly created projects references the user directory dynamically to better support multi-developer
 and source code control projects

- More sample programs
- Interrupts can now be triggered from AnalogTriggers and Digital inputs


      