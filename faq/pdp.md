---
layout: page
title: Power Distribution Panel (PDP) FAQ
permalink: /faq//pdp/
---

<img src = "../../Images/pdpinfo.png">

##Specs
12V Battery input (M6x1 Threaded Terminals)
8 - 12V 40A Unregulated Breaker Channels (accept up to XX awg wire)
8 - 12V 30A Unregulated Breaker Channels (accept up to XX awg wire

3 Dedicated 12V Unregulated Channels for VRM, PCM, and RoboRio

   - RoboRio on Dedicated 15A ATX Fuse
   - VRM and PCM on Shared 20A ATX Fuse


CAN Bus for Sensor Monitoring

   - Current
   - Voltage
   - Temperture
 
---

##Can I Use the old PDP Board with the new Control System?
Refer to legal FRC rules for the official answer to this question. I don't imagine this will be legal for competition. The RoboRio requires a 6.8-16VDC input voltage for normal operation while the old PDP board provides regulated 24VDC out of the dedicated cRIO terminal (This is because the old cRIO was a 24V device while the new RoboRio is a 12V nominal device).

Now if you want to run some tests, or use this on a practice bot, you can safely power the RoboRio from one of the unregulated 30A wago power channels on the old PDB. The RoboRio takes in unregulated 12V battery voltage, so plugging it directly into a 12V channel on the old PDB will work and will not damage the RoboRio. BUT this should only be done for testing/practicing purposes and only if you do not have a new 2015 CTRE Power Distribution Board Available. 

Do not plug the RoboRio into the old PDB cRIO power port. See the [RoboRio Faq](/RoboRio/faq/roborio/) for more info.

---

##What is the sample rate of current monitoring?
The PDP sensor readings are put out on CANbus once every 25ms.

---

##What does the PDP monitor over CAN?
The PDP provides instantaneous current on each individual channel, voltage on each channel, and temperature of the PDP. Each value is updated at the rate specified above.

---

##Do I need to plug in the CAN connection for the PDP to work?
No. Using the CAN bus is not required for the PDP board to distribute power. It is only required if you wish to access the current/voltage sensor readings on each channel of the PDP. In order to access the can information two things must happen:

1. You properly connect the PDP to the RoboRio via CAN
2. You use the appropriate Labview or WPILib PDP CAN libraries to read the sensor values in your robot code.

---

##When we remove a 40A circuit breaker from the Power Distribution Board, we are having some difficulty. 
These are the exact same 30A and 40A fuse holders used on the old PDB.  I noticed that the first time the breaker is inserted it is a bit more difficult than subsequent insertions.  Allow for some break-in time. Insertions/Removals should get easier over time. 

---

##Do the three ports along the bottom of the PDP have current monitoring like the rest of the panel?

No. The PDP does not monitor those dedicated power outputs directly.
The PDP only monitors the current outputs of each (16) of the high power channels

* Short circuits detected on each of the (16) wago connectors
* The incoming battery voltage
* The internal PDP temperature
* Any over-temperature fault
 
There is no current/voltage monitoring of the PCM, VRM, or RoboRio dedicated ports.

Here are some work-arounds to measure the PCM, VRM, RoboRio:

* The PCM monitors compressor current, and faults for shorts and compressor over-current and can be accessed over can
* The DriveStation Battery Voltage Reading is directly from the RoboRio input voltage.
* There is no way to read any information from the VRM unless external voltage/current sensors are added by the team

---

##I have nothing connected to a channel, but the current reading is XXA?


If the current is small this is probably OK (small being 1.2A or less). The current is larger this can indicate something wrong with the current sensor reading chip. The PDP has 4 current sensors chips

[0-3] share a a current sensing chip
[4-7] share a a current sensing chip
[8-11] share a a current sensing chip
[12-15] share a a current sensing chip

If there is damage to the current sensing device itself, expect to see erroneous readings on the other channels sharing the sensor.


---


##What faults are monitored on the PDP?

Refer to the official documentation on the PDP []().

If the PDP is connected to the RoboRio via CAN, you can use the RoboRio webpage to view the status of any PDP faults. 

1. Log in to the RoboRio webpage (see [RoboRio FAQ](/RoboRio/faq/roborio))
2. Click on the CAN interface from the side menu
3. Select the PDP to view more information on the hardware
4. Use the Self-Test button to provide detailed information of all sensors on the PDP, including any faults
5. Double-clicking the self-test button will reset any stick faults.


---

##How can I access the PDP via the web interface?

If the PDP is plugged into the RoboRio via CAN, you can view the status of the PDP through the RoboRio's web interface.

Simply use any browser with the silverlight plugin to navigate to the RoboRio's IP address. From there you can see all CAN devices connected to the RoboRio, and view their available data.

You can use this web interface to read the current sensor readings of the PDP, review any faults, change its CAN ID number, and even upgrade it's firmware.


Note: 

1. The webdash needs about 5 seconds on boot up to scan all CAN Node. This means it is possible to load the webpage before all CAN devices are discovered. Use the browser refresh in order to populate all discovered CAN devices. 

2. When a NEW can node is installed while the website has already been loaded, the webpage will need to be refreshed to discover the new device.

3. If there is a conflict of multiple devices with the same ID on the CAN network, the webpage will notify you. A "blink" LED feature on the CAN page will help you physically identify which CAN device you are working on by flashing its LED repeatedly.

4. From the website standpoing, having multiple dissimilar CAN node with the same ID is harmless. I.E having a PCM, PDP, and Jaguar with ID of 1 is acceptable. If this happens the website will not indicate any error.

5. Having two or more CAN node of the same type and device ID will prevent your robot application from identifying one can device from another. This can happen when you have multiple PCMs or Multiple CAN Talons. The Website will indicate an error. By defailt all CTRE devices ship with an ID of 0. The website handles this gracefully, so you can see all the devices still, and change their ID accordingly. Use the "Blink LED" feature to physically identify which device you are working on. 

5. You will need to give each and every device on your CAN bus a unique ID (whether they are similar or dissimilar) so that you can use them successuly in your code. The above points were just to highlight the limitations and relaxations imposed by the RoboRio webpage when dealing with CAN devices.


---

##How can I upgrade the Firmware on the PDP

For Beta testing the Firmware for the PDP was provided by CTRE. To flash the PDP is very similar to flashing the RoboRio.

1. Connect the RoboRio to the PDP using CAN.
2. Power the System and launch the RoboRio website
3. Login as `admin`
4. If you have trouble with any of the above steps see the [RoboRio FAQ](/RoboRio/faq/roborio)
5. Select the CAN device icon
6. Select the PDP and click on Upgrade Firmware
7. Navigate to the PDP Firmware you would like to use and select being update.
 


---

##I have heard some connectors no longer fit on the PDP battery terminals?

The PDP include a protective cover over the battery input cables. This solves having to use electrical tape to cover exposed terminals on the main input cables to the PDP. We use 6 awg cable from our battery to the PDP. 

The connector we use on the PDP terminals are here: [battery terminal](http://www.andymark.com/product-p/am-0805.htm)
The crimp tool we use is here: [swedge tool]()
The cable we use is bought here: [battery cable]()

---

##What wire size/type should I use for the CAN Bus?
See [Electrical FAQ](/RoboRio/faq/electrical/)

---

