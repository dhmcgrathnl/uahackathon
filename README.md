# UAHS Learn-a-thon Parking Challenge Team Guide

## Challenge Problem Statement

With the new parking changes, finding available parking will be a challenge at UAHS. Your challenge: *build a model parking lot with available parking sensors to help drivers find open spots.*

## Table of Contents
1. [Problem Statement](#UAHS-Learn-a-thon-Parking-Challenge)
1. [Hardware](#Hardware)
1. [Arduinio Set Up](#Arduino-set-up)
1. [Raspberry Pi Set Up](#Raspberry-pi-0-set-up)
1. [Arduino Set Up](#Arduino-set-up)
1. [Writing the Code](#Writing-the-code)
1. [Adding Alexa](#Adding-Alexa)


## Hardware

There are two hardware platform options: 
1. Raspberry Pi Zero W
1. Arduino Uno

Circuit parts: 
* LED lights
* Object Proximity sensors 
* Amazon Echo Dots (may need to be shared) 
* Micro USB cables
* HDMI mini cables

Software: 
* Blynk platform https://www.blynk.cc/ 

## Arduino Set Up

* Download Arduino IDE https://www.arduino.cc/en/main/software 
* Verify sample in IDE to configure set up using tutorial on site. 

## Raspberry Pi 0 Set Up
For the below steps you will be writing in files on the root of a linux file system as interpreted by windows. Rasbian picks up these files when it boots.  **When editing these files, make sure you use 'lf' line endings as opposed to 'crlf'**.  If you use VSCode you will see this as a drop down in the bottom right hand corner of the editor.  Other editors have similar options.
 
### Flashing the SD Card
Follow the instructions on [this page](https://styxit.com/2017/03/14/headless-raspberry-setup.html) to get the OS loaded.  
* When you are downloading the OS, choose **Rasbian Lite**. 
* This will also have you setup a wifi connection and place a  marker file to start an ssh server. Here is a [Sample WPA file](https://github.com/kamahl437/hackfiles/blob/master/wpa_supplicant.conf).


### Enabling Remote over USB and IP Detection
After you have an os but before you take the card out, use these directions to to enable network over USB.

* Navigate to the part of the page that says 'Say Bonjour' and download the bonjour drivers.
* Navigate to 'Connect Your PC to Raspberry Pi Zero via USB' on [this page](https://www.makeuseof.com/tag/directly-connect-raspberry-pi-without-internet/) and follow their directions.

### Remoting into the Pi

* Take the card out and insert it in to your pi zero.  
* Insert a usb cable in to the port marked usb (not 'pwr in').
* If using over wifi get your ip address from the network admin and type:

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

## Adding Alexa



### Creating an AWS Lambda Function

The lambda function is what the skill calls when invoked. It will be where the call is made to the Blynk API to get the sensor data. The Alexa 'fact skill' template will be used as a starting point, then customized for this project. 

1. Log in to the [Nationwide AWS Console](https://blue-eagle.signin.aws.amazon.com/console). Username: `alexa-hacker` password (ask a coach)
1. Click `Services` at the top left. 
1. Search for 'lambda`. 
1. Click `Create function`.
1. Choose `Use a blueprint`.
1. Search for `alexa` and choose the the `factskill` blueprint.
1. **Make sure you are in the N.Virgina region!** (top-right)
1. Name the function. 
1. Choose `lambda_execute_lambda` existing role. 
1. Under configuration, add a trigger using `Alexa Skills Kit`. 
1. Scroll down and configure the trigger from the last step. Disable skill verification. Save. 
1. Note the ARN in the top right of the page. This will be used to associate the skill. 

### Creating an Alexa Skill

The Alexa Skill is where Alexa is configured to interpret commands. The 'fact skill' template will be used as a starting point, then customized for this project. 

1. Log in to [Amazon Alexa Developer Portal](http://developer.amazon.com/alexa). Username: `uaschoolslearnathon` password: (ask a coach)
1. Scroll down and click `create a skill` button. 
1. Click the `start a skill` button. 
1. Click `create skill` button. 
1. Name the skill `TeamXSkill` with the team's name or number as X. Leave `custom` and `provision your own settings`. Click next.
1. Select `Fact skill` template. 
1. On the left menu, select `endpoint`. 
1. Add the ARN from the lambda in the default region box and hit `Save Endpoints` in the top left. 

### Calling Blynk from the Lambda

Modify the fact skill in the Amazon Developer portal and in the AWS lambda to call the Blynk API. 

### Testing the Skill in the Browser

### Deploying the Skill to the Device
