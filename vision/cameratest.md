---
layout: page
title: Vision Processing Device Test (Work In Progress)
permalink: /vision/cameratest/
---



## 1.0 Introduction:

   In this article Team 2168 compares the performance of 3 popular embedded processors for Vision Processing for it is applicability to the First Robotics Competition.

   The purpose of this test is to help determine which approach is best suitable to a team depending on their needs.

## 1.1 Background information

   In this study we wish to understand the performance differences between different embedded devices and determine if there is a clear advantage in using one over the next for FRC. We will be studying the total time it takes to process images on each target. 
   
   In general the time to process a frame is comprised of:
 
 <div>
 \[
 \begin{array}{ll}
   & \text{time to capture frame from camera} \\
 + & \text{time to process frame} \\
 \hline
   & \text{Total Processing time per frame} \\
 \end{array}
 \]
 </div>
 
We can use the total time to process a frame to determine how many frames per second we can process on each device without missing frames.



## 1.2 Test Objectives:
In this test we will be focusing on 3 test scenarios:

  A. Beagle Bone Black - Off Board Processor
  B. Nvidia Jetson TK1 - Off Board Processor
  C. Vision on Roborio along side Robot Code

The reason we are focusing on these 3 devices is two fold:

1. These are the current embedded devices we have on hand
2. These devices all share a similar ARM Cortex processor

The tests herein will be conducted using the same source code, library versions, and camera settings. The purpose is to have an apples-to-apples comparison of the same source code's performance on each target device.

For each scenario there will be two subsets of test:

* Baseline performance test
  - Used to capture the best case scenario processing time and image downloading time.
  - Goal is to isolate the processing thread and frame capture thread to calculate times individually
* Live performance test
  - The images to be processes will be captured live from a connected IP camera so as to mimic a real FRC match. At no point will previously saved images or local files be used (we want image download time to be factored in as well).

Each test will be using the Axis M1011 Ethernet Camera. We will vary the camera settings and apply those settings to each target so as to find the optimal and maximum FPS, and image quality settings which maximize performance on each embedded device.

---
---

##2.0 Meet the hardware:

## 2.1 Beagle Bone Black


## 2.2 Jetson TK1


## 2.3 RoboRio


## 2.4 Axis M1011 IP Camera

Camera Settings:
Camera: Axis M1011 Ethernet Camera
Compression: 30
Constant Bit Rate: 30kbit/s
Color Level: 100 out of 100
Brightness: 25 out of 100
Sharpness: 100 out of 100
Contrast: 100 out of 100
WhiteBalance: Fixed Indoor
Exposure: 23 out of 100
Exposure control: Hold Current

The only items we varied was:

* Frame Size: 
	- 320 x 240
	- 640 x 480
	
* Frames Per Second
    - 10 fps
    - 20 fps
    - unlimited (30FPS max rate)
	

---
---

## 3.0 Test Apparatus:

## 3.1 Scenario A Test Apparatus:

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
- No other devices on networks



## 3.2 Scenario B Test Apparatus:

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


## 3.3 Scenario C Test Apparatus:

- RoboRio, and M1011 Camera are connected via hardware Ethernet using D-Link 1522 Rev B switch.
- M1011 Camera and D-Link are powered from 2015 Voltage Regulator Module
- VRM and RoboRio are powered from 2015 Power Distribution Panel
- PDP is powered by FRC Legal Battery
^
- RoboRio IP: 10.21.68.2
- M1011 IP: 10.21.68.90
- Development Computer: 10.21.68.101
- No other devices on network


## 3.4 Measurement Accuracy:

The performance measurements will be done internally in the code Using C++ RT library clock on each device:

Here is an example of how the measurements are taken within the code.

{% highlight java %}
#include <ctime>

clock_gettime(CLOCK_REALTIME, &start);
   //some process to measure
clock_gettime(CLOCK_REALTIME, &end);
cout << diffClock(start, end) <<endl;

//Where diffClock is defined as
double diffClock(timespec start, timespec end) 
{ 
  return (end.tv_sec - start.tv_sec) + (double) (end.tv_nsec - start.tv_nsec)/1000000000.0f; 
} 
{%  endhighlight %}


---
---

## 4.0 Source Code Description:

The vision code used is the exact source code we ran throughout 5 competition in the 2014 season on a Beaglebone white. The source has undergone no changes for these test other than adding/modifying the areas to be timed

The code has 5 threads:

  - 1st: Outgoing TCP Messages to RoboRio
  - 2nd: Incoming TCP Messages to RoboRio
  - 3rd: FFMPEG Video Capture of Camera
  - 4th: Image processing thread

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


## 4.1 Generic Code Optimizations:

- The code is compiled with GCC 4.6.3 with -o3 optimizations enabled
- NEON mfpu for floating point is enabled for all targets
- Specific target optimizations are not enabled
- All output is written to a file vs cout (file output is much faster)
- \n is used instead of endl (to avoid flushing the buffer each time) 

RoboRio and BeagleBone black are compiled with gcc 4.6.3 with softFP floating point operations, -03 code optimization, and NEON SIMD support

Jetson TK1 vision code is compiled with gcc 4.6.3 with hardFP floating point operations, -03 code optimizations, and NEON SIMD support
 
In all instances the CPU of the device was manually set to the highest clock-rate so performance would not be diminished by "on demand" CPU throttling built into the linux OS.
 
Also X11 forwarding has been enabled and a view window outputting the processed image is displayed on the Development computer

```
Check the server's sshd_config (normally /etc/ssh/sshd_config), and make sure the X11Forwarding option is enabled with the line 
X11Forwarding yes
```

 ## 5.0 Results
 
 ## 5.1 Scenario A Tests (BeagleBone):
 
 
 
 
 
## 5.2 Scenario B Tests (Jetson TK1):

## 5.2.1 Baseline Tests

On the Tegra we executed the Vision code while reading an image from the file. The image was a snapshot taken from the Axis camera of our vision target. The purpose of this test was to calculate the fastest rate we could process images without worrying about downloading first. The image is loaded into memory only once.
We ran the test for both 320 x 240 images and 640x480 images.

current CPU frequency is 2.32 GHz and all 4 cores are online

Below is the sample image we used for the test.

<img style="margin:0px auto;display:block" img src="../Images/image320x240.jpg">

We ran the test for two cases:
 - With X11 forwarding enabled
 - Without X11 forwarding enabled
 
 The reason we did this was because, during our testing last year, we used X11 forwarding to view the image output while debugging/testing our algorithm, and it was notably slower than with X11 off. In a match, we do not use X11 forwarding.
 
 Below is a plot of how long each processing loop took to execute without X11 (blue) and with X11 (red).
 
 <img style="margin:0px auto;display:block" img src="../Images/320x240 Tegra Baseline Processing Speed (no X11).png">
 <img style="margin:0px auto;display:block" img src="../Images/320x240 Tegra Baseline Processing Speed (with X11).png">
 
 We can see that our processing time per frame on the Tegra took about 2.6ms nominally, and was under 3.4ms in the worst case. We also notice that when X11 is activated, our nominal processing time increases to about 4ms and peaks around 5ms in the worst case.
 
 
 NEED TO ADD FFMPEG BASELINE
 
 
 
## 5.2.1.1 640x480 Baseline processing

We ran the same test as above, but with a 640x480 image captured from the Axis. Below is the sample image we used for the test.

<img style="margin:0px auto;display:block" img src="../Images/image640x480.jpg" align="middle">

Just as before We ran the test for two cases:
 - With X11 forwarding enabled
 - Without X11 forwarding enabled
 
 
 Below is a plot of how long each processing loop took to execute without X11 (blue) and with X11 (red).
 
 <img style="margin:0px auto;display:block" img src="../Images/640x480 Tegra Baseline Processing Speed (no X11).png">
 <img style="margin:0px auto;display:block" img src="../Images/640x480 Tegra Baseline Processing Speed (with X11).png">
 
 We can see that our processing time per frame on the Tegra took about 10.3ms nominally, and was under 10.4ms in the worst case. We also notice that when X11 is activated, our nominal processing time increases to about 20ms and peaks around 22ms in the worst case.
 
 
 NEED TO ADD FFMPEG BASELINE
 

## 5.2 Scenario C Tests (RoboRio)

## 5.2.1 Baseline Tests

On the RoboRio we executed the Vision code while reading an image from the file. The image was a snapshot taken from the Axis camera of our vision target. The purpose of this test was to calculate the fastest rate we could process images without worrying about downloading first. The image is loaded into memory only once.
We ran the test for both 320 x 240 images and 640x480 images.

## 5.2.1.1 320 x 240 Baseline processing

Below is the sample image we used for the test.

<img style="margin:0px auto;display:block" img src="../Images/image320x240.jpg">

We ran the test for two cases:
 - With X11 forwarding enabled
 - Without X11 forwarding enabled
 
 The reason we did this was because, during our testing last year, we used X11 forwarding to view the image output while debugging/testing our algorithm, and it was notably slower than with X11 off. In a match, we do not use X11 forwarding.
 
 Below is a plot of how long each processing loop took to execute without X11 (blue) and with X11 (red).
 
 <img style="margin:0px auto;display:block" img src="../Images/320x240baselineprocess_nox11.png">
 <img style="margin:0px auto;display:block" img src="../Images/320x240baselineprocess_x11.png">
 
 We can see that our processing time per frame on the Roborio took about 22ms nominally, and was under 40ms in the worst case. We also notice that when X11 is activated, our nominal processing time increases to about 29ms and peaks around 50ms in the worst case.
 
 When then disable the processing thread, and enable the FFMPEG image capture thread. This test captures live images from the Axis camera as quickly as possible. The framerate on the camera is set to unlimited, which means it will serve pictures at 30 fps. This test will show how long it takes our software to download and store into memory a single frame.
 Again we run the tests with X11 (blue) and without X11 (red) forwarding on.
 
  <img style="margin:0px auto;display:block" img src="../Images/320x240baselineffmpeg_nox11.png">
 <img style="margin:0px auto;display:block" img src="../Images/320x240baselineffmpeg_x11.png">
 
 We can see from the plot, that it takes a nominal time of about 33ms, and worst case of 45ms to download a frame, and load it into memory. When comparing the charts it doesn't appear that X11 forwarding affect the outcome. This makes sense because X11 forwarding should only be active when the process thread is running (serving our output image). So this is what we should expect.
 
 Just based on these numbers, we can calculate a target FPS we can successfully process with the system we have set up, without experiencing lag. In this case we choose to use the worst case numbers because if we use the nominal numbers, when ever our processing thread, or FFMPEG thread hits a peak in execution time, our framerate will fall behind and this will introduce lag. In addition, these logs were captured individually and don't account for any overhead processing time. So we want to be conservative. The next section shows total execution time for the complete application. 
 
  <div>
 \[
 \begin{array}{ll}
   & 45ms \text{(time to capture frame from camera)} \\
 + & 40ms \text{(time to process frame)} \\
 \hline
   & 85ms \text{Total Processing time per frame} \\
 \end{array}
 \]
 </div>
 
 <br><br>
 We convert this number to Frames per second:
   <div>
 \[
\frac{1}{0.085} = 11.76 \text{fps}
 \]
 </div>
 
 <br><br>
 
 This shows that under these conditions we can successfully process our 320x240 images at 11fps on the RoboRio.
 
 

## 5.2.1.1 640x480 Baseline processing

We ran the same test as above, but with a 640x480 image captured from the Axis. Below is the sample image we used for the test.

<img style="margin:0px auto;display:block" img src="../Images/image640x480.jpg">

Just as before We ran the test for two cases:
 - With X11 forwarding enabled
 - Without X11 forwarding enabled
 
 
 Below is a plot of how long each processing loop took to execute without X11 (blue) and with X11 (red).
 
 <img style="margin:0px auto;display:block" img src="../Images/640x480 RoboRio Baseline Processing Speed (no X11).png">
 <img style="margin:0px auto;display:block" img src="../Images/640x480 RoboRio Baseline Processing Speed (with X11).png">
 
 We can see that our processing time per frame on the Roborio took about 90ms nominally, and was under 110ms in the worst case. We also notice that when X11 is activated, our nominal processing time increases to about 140ms and peaks around 170ms in the worst case.
 
 The 640x480 has 4 times the pixel density of the 320x240 image. So it makes sense that the processing time is roughly 3 times larger for the 640x480. (It is not 4 times larger because the the time spent on the first 320x240 pixels are shared between both test cases, thus increasing the 640x480 case by only a factor of 3).
 
 When then disable the processing thread, and enable the FFMPEG image capture thread. This test captures live images from the Axis camera as quickly as possible. The framerate on the camera is set to unlimited, which means it will serve pictures at 30 fps. This test will show how long it takes our software to download and store into memory a single frame.
 Again we run the tests with X11 (blue) and without X11 (red) forwarding on.
 
 <img style="margin:0px auto;display:block" img src="../Images/640x480 RoboRio Baseline FFMPEG Frame Capture(no X11).png">
 <img style="margin:0px auto;display:block" img src="../Images/640x480 RoboRio Baseline FFMPEG Frame Capture Speed (with X11).png">
 
 We can see from the plot, that it takes a nominal time of about 33ms, and worst case of 53ms to download a frame, and load it into memory. When comparing the charts it doesn't appear that X11 forwarding affect the outcome. This makes sense because X11 forwarding should only be active when the process thread is running (serving our output image). So this is what we should expect.
 
 Just based on these numbers, we can calculate a target FPS we can successfully process with the system we have set up, without experiencing lag. In this case we choose to use the worst case numbers because if we use the nominal numbers, when ever our processing thread, or FFMPEG thread hits a peak in execution time, our framerate will fall behind and this will introduce lag. In addition, these logs were captured individually and don't account for any overhead processing time. So we want to be conservative. The next section shows total execution time for the complete application. 
 
  <div>
 \[
 \begin{array}{ll}
   & 45ms \text{(time to capture frame from camera)} \\
 + & 90ms \text{(time to process frame)} \\
 \hline
   & 135ms \text{Total Processing time per frame} \\
 \end{array}
 \]
 </div>
 
 <br><br>
 We convert this number to Frames per second:
   <div>
 \[
\frac{1}{0.135} = 7.4 \text{fps}
 \]
 </div>
 
 <br><br>
 
 This shows that under these conditions we can successfully process our 640x480 images at 7fps on the RoboRio.
 