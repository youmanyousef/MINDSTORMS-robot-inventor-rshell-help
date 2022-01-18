# How to connect to your LEGO Mindstorms hub.
This page is in progress, not complete. I will come by periodically to update some information.

This LEGO mindstorms kit uses micropython as its os, so we can use rshell to connect to it.
First thing to do is to open a terminal (I dont know how to do this on windows) or connect to it using SSH, personally using a raspberry 4b.

## Python 3
[Get rshell](https://github.com/dhylands/rshell)
```bash
pi@raspberrypi:~ $ python3 -m pip install rshell
```
After its done installing, open a new terminal or reboot in some cases.
```bash
pi@raspberrypi:~ $ rshell
```
Make sure your device is plugged in via USB.
Most times it will connect if it detects it but if it doesnt, exit the rshell and try these commands
```bash
pi@raspberrypi:~ $ dmesg
-snip-
[ 3927.889850] usb 1-1.1: Product: LEGO Technic Large Hub in FS Mode
[ 3927.889863] usb 1-1.1: Manufacturer: LEGO System A/S
[ 3927.889875] usb 1-1.1: SerialNumber: 3374396F3338
[ 3927.983365] cdc_acm 1-1.1:1.0: ttyACM0: USB ACM device
-snip-
```
Now reopen rshell
```bash
/home/pi> connect serial ttyACM0
/home/pi> repl
Entering REPL. Use Control-X to exit.
>
MicroPython v1.14-893-gbae6ff2ee on 2021-11-04; LEGO Technic Large Hub with STM32F413xx
Type "help()" for more information.
>>>
```

We are done! now you have more control of your lego brick. Now you can manually import libraries and do usual micropython stuff.
Beware, the brick only has 27.75 MB of flash so dont go ham. 
[How i figured that out](https://www.geeksforgeeks.org/python-os-statvfs-method/)
```python
>>> import os
>>> storage = os.statvfs('/')
>>> print(storage[4] * storage[1] / 1024 / 1024) # in megs
27.75
```
