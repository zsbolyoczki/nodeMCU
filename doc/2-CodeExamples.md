# nodeMCU code examples





## 1. LUA prompt

Connect the board to the PC and open it with screen
```
screen /dev/ttyUSB0 115200
```

On the blank screen press Enter and the Lua prompt appears.



## 2. Wifi connection

This code connects the board to a WIFI network and prints the IP

```
wifi.setmode(wifi.STATION)

wifi.sta.sethostname("homero")
  
wifi.sta.config {ssid="SSID-NAME", pwd="WIFI-PASSWORD12"}

ip, nm, gw=wifi.sta.getip()

print("\nIP Info:\nIP Address: "..ip.." \nNetmask: "..nm.." \nGateway Addr: "..gw.."\n")
```

From now on the "ip", "nm" and "gw" variables are set until the board is rebooted.



## 3. Listen on a tcp port




## 4. Connect to a HTTP server and opening an URL



## 5. Temperature reading with a DS18B20 1-wire digital thermometer


Enable "LUA_USE_MODULES_DS18B20" in the nodemcu firmware in app/include/user_modules.h (remove the "//" from the beginning of the line.)

Recompile and flash the firmware.


https://roboindia.com/tutorials/ds18b20_temp_sensor_nodemcu









