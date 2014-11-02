##



##Set Static IP
Edit files /etc/network/interfaces



##Add Support for 32-bit files
1. sudo dpkg --add-architecture i386
2. sudo apt-get update
3. sudo apt-get install libc6:i386 libncurses5:i386 libstdc++6:i386


##Run Angstrom Executable (BeagleBone/BBB) on Jetson
1. copy executable `sudo rsync -avzhe ssh  kevin@10.21.68.104:/home/kevin/git/BeagleVision/Debug/* /home/BeagleVision/`
In order to run an executable cross-compiled for the ARM BB on the Jetson, we need to move one of the lib files. If you do not run this command, when trying to run your executable you may get the `no such directory of file` bash error which is not very helpful. After running this command your previous executable should run. 

1. `sudo cp /lib/arm-linux-gnueabihf/ld-linux.so.3 /lib/`
2. Copy OpenCV libraries to jetson preserving symlinks `sudo rsync -avzhe ssh  kevin@10.21.68.104:/home/OpenCVArm/opencv/platforms/linux/build_hardfp/install/lib/* /usr/local/lib/openCV2.4/`
3. add location of openCV .so to linker path `sudo vi /etc/ld.so.conf.d/beaglevision.conf`
4. hit `i` on keyboard to enter `insert` mode
5. add 
```
/lib/arm-linux-gnueabihf
/usr/local/lib/openCV2.4
```
6. hit `esc` to exit insert mode
7. hit `:wq` to save
8. run  `sudo ldconfig` to update ldd

