##



##Set Static IP
Edit files /etc/network/interfaces



##Add Support for 32-bit files
1. sudo dpkg --add-architecture i386
2. sudo apt-get update
3. sudo apt-get install libc6:i386 libncurses5:i386 libstdc++6:i386


##Run Angstrom Executable (BeagleBone/BBB) on Jetson
In order to run an executable cross-compiled for the ARM BB on the Jetson, we need to move one of the lib files. If you do not run this command, when trying to run your executable you may get the `no such directory of file` bash error which is not very helpful. After running this command your previous executable should run. 

1. `sudo cp /lib/arm-linux-gnueabihf/ld-linux.so.3 /lib/`

