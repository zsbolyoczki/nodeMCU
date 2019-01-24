# nodeMCU dev environment


This document is about to set up the nodeMCU ESP8266 WIFI board with 4M flash on Linux Mint 19.1 (and probably all similar distros) and flash the board with a firmware.



## 1. Connect the board to your PC and check if the device is functioning


This will display the serial port the device is attached to
```    
dmesg | egrep "cp210x converter now attached to tty"
```

Just double check if it is really there:
```
lsusb | grep -i "cp210"
```


## 2. Modify membership


Add yourself to the dialout group to upload the firmware to the device
```
sudo adduser ${USER} dialout
```


## 3. Create the work dirs
```
cd 
mkdir -p work/nodeMCU
cd work/nodeMCU
```


## 4. Install basic OS packages
```
sudo apt install -y make unrar autoconf automake libtool gcc g++ gperf flex bison help2man texinfo gawk ncurses-dev libexpat-dev python python-serial sed git libtool-bin screen
```


## 5. Get luatool

luatool is used to upload compiled binaries to the board.
```
git clone https://github.com/4refr0nt/luatool.git
```


## 6. Get and compile the ESP SDK

Download it with all the other repos included (it may take some time)
```
cd ~/work/nodeMCU
git clone --recursive https://github.com/pfalcon/esp-open-sdk.git
```

This really takes a lot of time
```
cd esp-open-sdk
make clean
make # this is the same as make STANDALONE=y
```

At the end of the process the new PATH env is displayed.
Add it to your current one.


## 7. Get and compile the NodeMCU firmware

Get the source
```
cd ~/work/nodeMCU
git clone --recurse-submodules https://github.com/nodemcu/nodemcu-firmware.git
```

Disable unnecessary modules to spare some RAM
```
cd nodemcu-firmware
vim app/include/user_modules.h
```

Add your own version number if you want by editing app/include/user_version.h


Finally compile the firmware (1-2 min)
```
cd ~/work/nodeMCU/nodemcu-firmware
make clean && make
```


## 8. Flash the board with the firmware

If everything went well the firmware is in the bin directory.
To send it to the board run
```
make flash4m 
```

Try to connect to the board
```
screen /dev/ttyUSB0 baudrate
```

Press the "USER" button on the board (also called "RST").
Board layout can be seen here: https://www.cnx-software.com/wp-content/uploads/2015/10/NodeMCU_v0.9_Pinout.png

After reset a lot of garbage appears on the screen then the nodeMCU Lua prompt.
If that prompt doesn't appear after a short time repeat the process with different baud rate (2400, 4800, 9600, 19200, 38400, 57600, 115200).
If nothing helps, repeat the flashing.

You can leave the screen with "CTRL-A K" (or just detach with "CTRL-A D").





