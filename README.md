# UAHS Learn-a-thon Parking Challenge

## The Challenge

With the new parking changes, finding available parking will be a challenge at UAHS. Your challenge: *build a hardware or software model solution that can help drivers find available parking spots!*

## Table of Contents
1. [Problem Statement](#UAHS-Learn-a-thon-Parking-Challenge)
1. [Hardware](#Hardware)
1. [Arduinio Set Up](#Arduino-set-up)
1. [Raspberry Pi Set Up](#Raspberry-pi-0-set-up)
1. [Arduino Set Up](#Arduino-set-up)
1. [Writing the Code](#Writing-the-code)


## Hardware

There are two hardware platform options: 
1. Raspberry Pi Zero W
1. Arduino Uno

Available hardware: 
* LED lights
* Object Proximity sensors 
* Amazon Echo Dots (may need to be shared) 
* Micro USB cables
* HDMI mini cables

Available software: 
* Blynk platform https://www.blynk.cc/ 

## Arduino Set Up

* Download Arduino IDE https://www.arduino.cc/en/main/software 
* Verify sample in IDE to configure set up using tutorial on site. 

## Raspberry Pi 0 Set Up
For the below steps, you will be writing in files on the root of a linux file system as interpreted by windows.  It looks strange but rasbian knows what to do once it boots.  **when you are writing these files you use 'lf' line endings as opposed to 'crlf'**.  If you use VSCode you will see this as a drop down in the bottom right hand corner of the editor.  Other editors have similar options
 
### Flashing the SD Card
Follown the instructions on [this page](https://styxit.com/2017/03/14/headless-raspberry-setup.html) to get the OS loaded.  

When you are downloading the OS, choose **Rasbian Lite**. 
This will also have you setup a wifi connection and place a  marker file to start an ssh server. Here is a [Sample WPA file](https://github.com/kamahl437/hackfiles/blob/master/wpa_supplicant.conf).


### Enabling Remote over USB and IP Detection
After you have an os but before you take the card out, use these directions to to enable network over USB.
navigate to the part of the page that says 'Say Bonjour' and download the bonjour drivers.
After this navigate to 'Connect Your PC to Raspberry Pi Zero via USB' and follow their directions.
https://www.makeuseof.com/tag/directly-connect-raspberry-pi-without-internet/

### Remoting into the Pi
Take the card out and insert it in to your pi zero.  Insert a usb cable in to the port marked usb (not 'pwr in').
If using over wifi get your ip address from the network admin and type:

`ssh pi@{pi ip address}`

password will be `raspberry`

If using over usb type:

`ssh pi@raspberrypi.local`

password will be `raspberry`.

## Writing the Code
### Python
https://raspberrypihq.com/making-a-led-blink-using-the-raspberry-pi-and-python/

### Java (Harder setup)
https://github.com/kamahl437/hackfiles/blob/master/javasetup.md

