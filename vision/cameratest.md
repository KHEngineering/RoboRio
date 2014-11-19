---
layout: page
title: Vision Processing Device Test
permalink: /vision/cameratest/
---



Introduction:
In this article Team 2168 compares the performance of 3 popular embedded processors for Vision Processing for it is applicability to the First Robotics Competition.
The purpose of this test is to help determine which approach is best suitable to a team depending on their needs.

Test Objectives:
In this test we will be focusing on 3 test scenarios:

  A. Beagle Bone Black - Off Board Processor
  B. Nvidia Jetson TK1 - Off Board Processor
  C. Vision on Roborio along side Robot Code

The reason we are focusing on these 3 devices is two fold:

1. These are the current embedded devices we have on hand
2. These devices all share a similar ARM Cortex processor

The tests herein will be conducted using the same source code, library versions, and camera settings. The purpose is to have an apples-to-apples comparison of the same source code's performance on each target device.


The images to be processes will be captured live from a connected IP camera so as to mimic a real FRC match. At no point will previously saved images or local files be used (we want image download time to be factored in as well).
Each test will be using the Axis M1011 Ethernet Camera. We will vary the camera settings and apply those settings to each target so as to find the optimal and maximum FPS, and image quality settings which maximize performance on each embedded device.



Meet the hardware:
###Beagle Bone Black


###Jetson TK1


###RoboRio


###Axis M1011 IP Camera
30FPS max rate

Test Apparatus:
Scenario A Test Apparatus:

- BeagleBone Black, RoboRio, and M1011 Camera are connected via hardware Ethernet using  D-Link 1522 Rev B switch.
- M1011 Camera and D-Link are powered from 2015 Voltage Regulator Module
- VRM and RoboRio are powered from 2015 Power Distribution Panel
- PDP is powered by FRC Legal Battery
- BeagleBone Black is powered from 5v2A supply connected to 110V wall outlet
^
- BeagleBone Black IP: 10.21.68.33
- RoboRio IP: 10.21.68.2
- M1011 IP: 10.21.68.90
- Development Computer: 10.21.68.101
- No other devices on network

<img src="{{site.baseurl}}/vision/cameratest/320x24010fps.png">

---

Scenario B Test Apparatus:

- Jetson TK1, RoboRio, and M1011 Camera are connected via hardware Ethernet using D-Link 1522 Rev B switch.
- M1011 Camera and D-Link are powered from 2015 Voltage Regulator Module
- VRM and RoboRio are powered from 2015 Power Distribution Panel
- PDP is powered by FRC Legal Battery
- Jetson TK1 is powered from 12v5A external supply connected to 110V wall outlet
^
- Jetson TK1 IP: 10.21.68.71
- RoboRio IP: 10.21.68.2
- M1011 IP: 10.21.68.90
- Development Computer: 10.21.68.101
- No other devices on network



---

Scenario C Test Apparatus:

- RoboRio, and M1011 Camera are connected via hardware Ethernet using D-Link 1522 Rev B switch.
- M1011 Camera and D-Link are powered from 2015 Voltage Regulator Module
- VRM and RoboRio are powered from 2015 Power Distribution Panel
- PDP is powered by FRC Legal Battery
^
- RoboRio IP: 10.21.68.2
- M1011 IP: 10.21.68.90
- Development Computer: 10.21.68.101
- No other devices on network




Measurement Accuracy:

The performance measurements will be done internally in the code Using C++ RT library clock

Here is an example of how the measurements are taken within the code.

{% highlight java %}
#include <ctime>

clock_gettime(CLOCK_REALTIME, &start);

   //some process to measurve

clock_gettime(CLOCK_REALTIME, &end);

cout << diffClock(start, end) <<endl;


//Where diffClock is defined as
double diffClock(timespec start, timespec end) 
{ 
  return	(end.tv_sec - start.tv_sec) + (double) (end.tv_nsec - start.tv_nsec)/ 1000000000.0f; 
} 
{%  endhighlight %}

Source Code Description:

The vision code used is the exact source code we ran throughout 5 competition in the 2014 season on a Beaglebone white. The source has undergone no changes for these test other than adding/modifying the areas to be timed

The code has 5 threads:

  1st: Outgoing TCP Messages to RoboRio
  2nd: Incoming TCP Messages to RoboRio
  3rd: FFMPEG Video Capture of Camera
  4th: Image processing thread

The program is written using pthread and pthread mutex locks for thread safe operation.
Upon startup the Outgoing TCP link and FFMPEG threads start and try to establish communication with the RoboRIo and the IP
camera respectively.

Once communication with the RoboRio is established, the Incoming TCP message thread starts, if there is no communication with
the RoboRio the outgoing thread will retry 5 times a second

In parallel, the FFMPEG thread is trying to establish a link with the IP Camera. IF no link is established the thread will
retry at a rate of 1 time a second.

Once the camera is established, the thread flushes all images for 12 seconds. This means the thread just grabs the frame and
throws it away. This is to ensure that there is no buffered/old images stored in the camera's network buffer during camera
startup.

After the 12 second flush, the Imagine processing thread will start and the FFMPEG thread will capture each frame and store
it in a thread safe global variable. Each loop iteration, the FFMPEG overwrites the previous frame captured.

Each processing loop, the thread will grab the latest FFMPEG frame and perform the following OPENCV operations:

- InRange Threshold
- Blur filter
- findContors
- Box all Contours
- Determine Size ratio and position of all contours (for Hot target detection)

After which the processing image is done, and a few global thread safe variables are updated based on what the image
processing determine which are then sent over the outgoing TCP message to the RoboRio

Then the process Image continues, all while FFMPEG continues to grab the latest frame from the camera in parallel.


Generic Code Optimizations:
The code is compiled with GCC 4.6.3 with -o3 optimizations enabled
NEON mfpu for floating point is enabled for all targets
Specific target optimizations are not enabled
All output is written to a file vs cout (file output is much faster)
\n is used instead of endl (to avoid flushing the buffer each time) 

RoboRio and BeagleBone black are compiled with gcc 4.6.3 with softFP floating point operations, -03 code optimization, and NEON SIMD support
Jetson TK1 vision code is compiled with gcc 4.6.3 with hardFP floating point operations, -03 code optimizations, and NEON SIMD support
 
In all instances the CPU of the device was manually set to the highest clock-rate so performance would not be dimminshed by "on demand" CPU throttling built into the linux OS.
 

Also X11 fowarding has been enabled and a view window outputting the processed image is displayed on the Development computer

```
Check the server's sshd_config (normally /etc/ssh/sshd_config), and make sure the X11Forwarding option is enabled with the line 
X11Forwarding yes
```

 
 Scenario A Tests:
 
 
 
 
 
Scenario B Tests:


Camera Settngs:
Camera: Axis M1011 Ethernet Camera
Frame Size: 320 x 240
Compression: 0
FPS: 10 frames
Constant Bit Rate: 30kbit/s
Color Level: 100 out of 100
Brightness: 25 out of 100
Sharpness: 100 out of 100
Contrast: 100 out of 100
WhiteBalance: Fixed Indoor
Exposure: 23 out of 100
Exposure control: Hold Current



current CPU frequency is 2.32 GHz.


<Sample of Image>


Results after 5 mins, with x window:
Avg FFMPEG Time Per Frame0.0746527seconds
Avg processing time: 0.0707223 seconds


Results after 5 mins, without x window:
Avg FFMPEG Time Per Frame0.0716247seconds
It took 0.077824 seconds to process frame
 Avg processing time: 0.0773571 seconds

No noticable lag behind real-time

---------

FPS: 20 FPS
Constant Bit Rate: Unlimited

Results After 5 mins, with x Window
Avg FFMPEG Time Per Frame0.0242383seconds
Avg processing time: 0.0193759 seconds

Results After 5 mins, without X window
Avg FFMPEG Time Per Frame0.0242099seconds
It took 0.0127431 seconds to process frame
 Avg processing time: 0.025629 seconds


No noticeable lag behind real-time


---------

FPS: Unlimited
Constant Bit Rate: UnlimitedAvg processing time: 0.0781722 seconds
It took FFMPEG 0.0390107 seconds to grab stream 
Avg FFMPEG Time Per Frame0.0320678seconds
It took FFMPEG 0.0252596 seconds to grab stream 
Avg FFMPEG Time Per Frame0.0320673seconds
It took FFMPEG 0.0361694 seconds to grab stream 
Avg FFMPEG Time Per Frame0.0320676seconds

Running loops without any wait

Results after 5 mins, with x Window:
Avg processing time: 0.0781722 seconds
It took FFMPEG 0.0390107 seconds to grab stream 
Avg FFMPEG Time Per Frame0.0320678seconds
It took FFMPEG 0.0252596 seconds to grab stream 
Avg FFMPEG Time Per Frame0.0320673seconds
It took FFMPEG 0.0361694 seconds to grab stream 
Avg FFMPEG Time Per Frame0.0320676seconds


Results after 5 mns, without X window:
 Avg processing time: 0.107181 seconds
It took FFMPEG 0.030361 seconds to grab stream 
Avg FFMPEG Time Per Frame0.0317515seconds
It took FFMPEG 0.0332003 seconds to grab stream 
Avg FFMPEG Time Per Frame0.0317517seconds
It took FFMPEG 0.0321802 seconds to grab stream 
Avg FFMPEG Time Per Frame0.0317517seconds
It took 0.0989493 seconds to process frame
 Avg processing time: 0.107178 seconds


Processed image would lag behind processed image, and catch back up, but lag was noticable. On average lag was a greater than 500ms with frequent delays greater than 1 second.

<sample pic>










