# WirelessCarPlay
Wireless CarPlay for CarPlay enabled cars. 
Compatible with Raspberry Pi 5 Debian GNU/Linux 13.3 (trixie) 

# Basics

Assume that you have Carplay enabled car (full list of car models can be
found here: https://www.apple.com/ios/carplay/available-models/). But most
of them only allow you to use wired connection. It's OK during long distance
trips (you can power up your battery) but very inconvenient when driving short
journeys.

# Idea behind this code

The whole idea is to use Raspberry Pi hardware which will be connected to the USB
port (Carplay enabled port) and your iPhone will use Bluetooth and WiFi connection to the RPi.
This software will take care of BLE and WiFi connection and pass all data to
your head unit via USB port.

# Compilation

1. mDNSResponder
Before compile CarPlay must be compiled mDNS so we must starts here.
```
cd mDNSResponder/mDNSPosix
make os=linux
sudo make os=linux install

```

2. CarPlay 
```
cd source/PlatformPOSIX
make os=linux clean
make os=linux verbose=1 
sudo cp ../build/Release-linux/*.so /usr/lib/
sudo cp ../build/Release-linux/airplayutil /usr/bin/
```

3. Compile example AppleCarplay_AppStub.c 
```
cd source/Examples
make
```

