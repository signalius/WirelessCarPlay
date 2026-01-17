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

# Test MFI 3959 chip
There are some rumors on Internet that is necessary to slow down I2C for MFI chip by using dtoverlay:
```
sudo dtoverlay i2c-gpio,bus=2,i2c_gpio_sda=2,i2c_gpio_scl=3,i2c_gpio_delay_us=50
```
However I see that is noc necessary and you can use /dev/i2c-1 with normal speed.

To test MFI chip you have to execute ```airplayutil mfi``` like here:

```
$ sudo airplayutil mfi
MFi initialize.
I2C Device addr: 10
Interface: /dev/i2c-1
Init time: 103 ms
Certificate (0 ms):

+0000: 30820388 06092a86 4886f70d 010702a0 |0^^^^^*^H^^^^^^^| (908 bytes)
+0010: 82037930 82037502 01013100 300b0609 |^^y0^^u^^^1^0^^^|
+0020: 2a864886 f70d0107 01a08203 5d308203 |*^H^^^^^^^^^]0^^|
+0030: 59308202 41a00302 0102020f 2222aa15 |Y0^^A^^^^^^^""^^|
+0040: 0817aa06 aa9007aa 16780930 0d06092a |^^^^^^^^^x^0^^^*|
+0050: 864886f7 0d010105 05003081 83310b30 |^H^^^^^^^^0^^1^0|
+0060: 09060355 04061302 55533113 30110603 |^^^U^^^^US1^0^^^|
+0070: 55040a13 0a417070 6c652049 6e632e31 |U^^^^Apple Inc.1|
+0080: 26302406 0355040b 131d4170 706c6520 |&0$^^U^^^^Apple |
+0090: 43657274 69666963 6174696f 6e204175 |Certification Au|
+00A0: 74686f72 69747931 37303506 03550403 |thority1705^^U^^|
+00B0: 132e4170 706c6520 69506f64 20416363 |^.Apple iPod Acc|
+00C0: 6573736f 72696573 20436572 74696669 |essories Certifi|
+00D0: 63617469 6f6e2041 7574686f 72697479 |cation Authority|
+00E0: 301e170d 31353038 31373230 34363239 |0^^^150817204629|
...
```



