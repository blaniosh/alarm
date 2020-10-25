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

[Read More](https://github.com/blaniosh/alarm/wiki)

## Operation
Wireless key remote pressed for 4 or more seconds > Alarm set if previously unset or unset if previously set.

Correct passcode entered into web form > Alarm set if previously unset or unset if previously set, Web page updates after countdown period (exit time of 36 seconds or 7 seconds on entry).

Alarm unset > After countdown period, webpage displays green box and button shows “SET”, Email sent stating Alarm has been unset

Alarm set > After countdown period, webpage displays blue box and button shows “UNSET”, Email sent stating Alarm has been set, LED is ON

Alarm triggered > Webpage displays, ** ALARM TRIGGERED **, red box and button shows “RESET”, Email sent stating Alarm has been triggered, LED FLASHES
![Webpage status](https://github.com/blaniosh/alarm/blob/main/status.jpg)

## Module
ESP-32S Development board utilising Wifi, three inputs, two outputs, internal LED, email server and over the air (OTA) firmware update. 

Software written in Arduino IO (C++) and based on existing templates – See acknowledgements. Software was based on published projects and modified to suit.  It was tested using components on a breadboard.
## Hardware 
Interface – Veroboard with MP2307 12v to 5v DC/DC converter, 2NAAAAA npn transistor, six resistors (6.7K (2), 10K (2), 1K and 330 Ohm, 817 Optocouplers (3); 433mhz relay module receiver, two remotes and a 10K resistor.

The interface is fitted inside a small plastic wallet and placed inside the alarm case along with the wireless remote receiver. 

The ESP-32 is mounted on veroboard and placed in small, clear rectangular box. It has been mounted adjacent to the alarm panel. 
## Alarm Panel Connections (5)
1) 12v 
2) 0V; 
3) Key switch in biased mode (12v when closed for a minimum of 1 second will set/unset the alarm) 
4) SW latch (0v if alarm unset, 12v if set) 
5) Bell (0v if triggered, 12v if not)
## ESP-32 Connections (7)
1) 3.3v 
2) VIN (5v) 
3) 0v 
4) GPIO22 (wireless remote) 
5) GPIO19 (alarm state – set or unset) 
6) GPIO23 (set/unset the alarm) 
7) GPIO18 (bell triggered)
![Hardwire](https://github.com/blaniosh/alarm/blob/main/alarm%20breadboard.jpg?raw=true)

## Issues/comments
_Location of interface_ - It was decided to keep the interface separate from the ESP-32 in order to keep the 12v alarm panel wiring discreet from the 3.3/5v wiring of the ESP-32.

_Wireless remote random operation_ - The wireless remote control receiver suffered from random triggers (probably from stray RF) resulting in the alarm being set/unset by itself. In order to resolve this, the output from the remote relay was fed into GPIO22 of the ESP-32 and a time condition set (currently 4 seconds but adjustable) before the state was changed. A better solution would be to use a different remote relay which doesn’t suffer from random triggers and could be connected directly (it outputs 12v) to the key switch.

_Wifi receiver of the ESP-32_ – A powerline adapter and unused router have been used to provide wireless access to the garage. The following site suggests ways to improve the Wifi reception of the ESP module - https://www.hackster.io/rayburne/esp32-development-board-official-vs-clone-7f4ff7

_Elegant OTA_  - This is a beautifully crafted and simple way to update ESP-32 firmware without having to disconnect the module and connect to USB. I did have problems updating scripts when the Wi-Fi connection was less than optimal.
## Acknowledgements
Rui Santos https://randomnerdtutorials.com/esp32-esp8266-input-data-html-form the HTML input data

Ayush Sharma  https://github.com/ayushsharma82/AsyncElegantOTA for the slick and streamlined Async Elegant OTA updater

Surviving with Android https://www.survivingwithandroid.com/send-email-using-esp32-smtp-server  for the send mail with SMTP email server

ESP32-Mail-Client https://github.com/mobizt/ESP32-Mail-Client 

ESPAsyncWebServer https://github.com/me-no-dev/ESPAsyncWebServer 

AsyncTCP https://github.com/me-no-dev/AsyncTCP    
## Images   
![The Gardiner 800 Alarm](https://github.com/blaniosh/alarm/blob/main/IMG_20200922_122825.jpg)
The Gardiner 800 Alarm
![The interface](https://github.com/blaniosh/alarm/blob/main/IMG_20201004_110607.jpg)
The Interface
![Mounting the interface](https://github.com/blaniosh/alarm/blob/main/IMG_20201004_150928.jpg)
Mounting the interface
![The original wireless remote module - suffers from random triggers](https://github.com/blaniosh/alarm/blob/main/IMG_20201004_151739.jpg)
The original wireless remote module - suffers from random triggers
![The second remote receiver](https://github.com/blaniosh/alarm/blob/main/IMG_20201013_110852.jpg)
The second remote receiver, that doesn't appear to suffer random triggers.
![The ESP-32 mount](https://github.com/blaniosh/alarm/blob/main/IMG_20201022_154156.jpg)
The ESP-32 mount
![The ESP-32 mount](https://github.com/blaniosh/alarm/blob/main/IMG_20201022_112512.jpg)
The ESP-32 mounted
