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

Installing the JVM for Embedded Devices, is not the same as install the JVM on a desktop. Oracle, the developers of the Java Virtual Machine for Embedded devices decided to release the JVM with a special installation procedure. The user must download the JVM to a host computer and run a program which builds an embedded JVM for your target with all of the configurations you desire. Then, you transfer the built JVM to your target (embedded device).

FIRST has created an easy to follow process that does all of the configurations for you, and runs the commands to build the JVM for you so that you do not need to be concerned with the details. Follow their directions below. If you wish to do it on your own, I am working on posting the manual steps required.

###Official FIRST Procedure
Ensure RoboRio is flashed and Imaged to latest versions then continue with [Offical screensteps directions](https://wpilib.screenstepslive.com/s/4485/m/13809/l/243933-installing-java-8-on-the-roborio-java-only)

###Manual Procedure
1. Create an account on Oracles Website [oracle](https://login.oracle.com/mysso/signon.jsp)
2. Download the Java SE 8 Embedded JVM for ARMv7 Linux VFP, SoftFP ABI, Little Endian [ARM JVM](http://www.oracle.com/technetwork/java/embedded/embedded-se/downloads/javase-embedded-downloads-2209751.html)
3. Use 7-zip to untar the download on your host machine

TO BE CONTINUED

---

##Can I see live Program Output in Eclipse?

Yes. Use the RioLog Viewer.

To find the RIOLog window, in eclipse, go to Window, Show View, Other and search for RIOlog and you'll see it. Once you add it, it will stay around between eclipse restarts.

---

##Can I use an older version of Eclipse like Kelper with the plugins?
Yes, but only with a Java v7 or earlier JDK. There is a ANT build bug in older version of eclipse where the default ANT build version that ship with the older eclipse versions do not recognize Java v8.

See the bug report here: [bug](https://wiki.eclipse.org/Ant/Java8)

We recommend using Eclipse Luna where ever possible, with JDK v8, but if you must use Kepler, downgrade the JVM to v7 or run the fix noted in the bug report to use JVM v8 with Eclipse Kepler. 

---

##When I deploy code, where is it saved on the RoboRio?

User programs are downloaded to /home/lvuser directory

---

##When I open eclipse I get an error stating "Unable to find JVM"

This problem is most likely caused by not having a JVM or JDK installed on your computer. Please install a JVM on your programming computer in accordance with step 4 of the quick start guide above.

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

1. Use find to determine where the JVM is located. Run `find / -name *jar*` in the Roborio termina. The `jar` application must be in the location `/usr/local/frc/JRE/bin`
2. Once the JVM is in the right folder location ensure the execute attribute is set `chmod +x /usr/local/frc/JRE/bin/*`

---

##Can you tell me whats new between 2014 Java and 2015 Java WPILib

- This list is a work in progress and will be provided soon


      
