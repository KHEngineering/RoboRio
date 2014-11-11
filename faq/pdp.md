---
layout: page
title: Power Distribution Panel (PDP) FAQ
permalink: /faq//pdp/
---


##Specs
12V Battery input (M6x1 Threaded Terminals)
8 - 12V 40A Unregulated Breaker Channels (accept up to XX awg wire)
8 - 12V 30A Unregulated Breaker Channels (accept up to XX awg wire
3 Dedicated 12V Unregulated Channles for VRM, PCM, and RoboRio
 - RoboRio on Dedicated 15A ATX Fuse
 - VRM and PCM on Shared 20A ATX Fuse
CAN Bus for Sensor Monitoring
 - Current
 - Voltage
 - Temp
 
---

##Can I Use the old PDP Board with the new Control System?
Refer to legal FRC rules for the official answer to this question. I don't imagine this will be legal for competition. The RoboRio requires a 7-16V input while the PDP board provides regulated 24V DC out of the cRIO terminal (This is because the old cRIO was a 24V device while the new RoboRio is a 12V nominal device).

Now if you want to run some tests, or use this on a practice bot, you can safely power the RoboRio from one of the unregulated 30A wago power channels on the old PDB. The RoboRio takes in unregulated 12V battery voltage, so plugging it directly into a 12V channel on the old PDB will work. - BUT This should only be done for testing/practicing purposes and only if you do not have a new 2015 CTRE Power Distribution Board Available. 

Do not plug the RoboRio into the old PDB cRIO power port. See the [RoboRio Faq](/RoboRio/faq/RoboRio/) for more info

---

##What is sample rate of current monitoring?
The PDP sensor readings are put out on CANbus once every 25ms.

---

##What does the PDP monitor over CAN?
The PDP provides instantaneous current on each individual channel, voltage on each channel, and temperature of the PDP. Each value is updated at the rate specified above.

---

##Do I need to plug in the CAN connection for the PDP to work?
No. Using the CAN bus is not required for the PDP board to distribute power. It is only required if you wish to access the current/voltage sensor readings on each channel of the PDP.

---

##When we remove a 40A circuit breaker from the Power Distribution Board, we are having some difficulty. 
These are the exact same 30A and 40A fuse holders used on the existing PDB.  I noticed that the first time the breaker is inserted it is a bit more difficult than subsequent insertions.  Allow for some break-in time. Insertions/Removals should get easier over time. 

---

##Do the three ports along the bottom of the PDP have current monitoring like the rest of the panel?

No. The PDP does not monitor those dedicated power outputs directly.
The PDP only monitors the current outputs of each (16) of the high power channels
* Short circuits detected on each of the (16) wago connectors
* The incoming battery voltage
* The internal PDP temperature
* Any over-temperature fault

The PCM monitors compressor current, and faults for shorts and compressor over-current.

---

##I have nothing connected to a channel, but the current reading is XXA?


---


##What is fault monitoring?


---

##How can I access the PDP via the web interface?

If the PDP is plugged into the RoboRio via CAN, you can view the status of the PDP through the RoboRio's web interface.

Simply use any browser with the silverlight plugin to navigate to the RoboRio's IP address. From there you can see all CAN devices connected to the RoboRio, and view their available data.
You can use this web interface to read the current sensor readings of the PDP, review any faults, and even upgrade it's firmware.

---

##I have heard some connectors no longer fit on the PDP battery terminals?

The PDP include a protective cover over the battery input cables. This solves having to use electrical tape to cover exposed terminals on the main input cables to the PDP. We use 6 awg cable from our battery to the PDP. 

The connector we use on the PDP terminals are here:[Battery Terminal]()
The crimp tool we use is here: [swedge tool]()
The cable we use is bought here: [battery cable]()

---

##What wire size/type should I use for the CAN Bus?
See [Electrical FAQ](/RoboRio/faq/electrical/

---

