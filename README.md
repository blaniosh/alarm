# Smart Alarm
This is a project to add additional ‘smart’ functionality into a thirty year old (1993) but fully functioning (and reliable) alarm system.
![](https://github.com/blaniosh/alarm/blob/main/intro.jpg)
## Existing alarm system
Gardiner Gardtec 800 series alarm, powered by 240v stepped down to 12v DC. With LED and LCD extension display/key pads.

4 wire detectors and 8 zones - with Texecom dual technology PIRS, a magnetic switch and a shock detector. Bell/Strobe unit and extension speakers.
## “Smart” functionality added
Set and Unset of alarm using a remote control or via a keycode entered into a local (for security reasons) webpage. The webpage is accessible when outside the LAN by using a VPN server running on a Raspberry Pi. The webpage is redirected from a local domain (alarm.domain.com).

Live status of system (unset, set or alarm triggered) via the internal LED, a webpage and an email notification.

Remote updateable of firmware using Elegant OTA.

## [Read More...](https://github.com/blaniosh/alarm/wiki)

