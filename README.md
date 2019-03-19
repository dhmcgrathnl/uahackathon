# UAHS Learn-a-thon Parking Challenge Team Guide

## Table of Contents
1. [Challenge Statement](#Challenge-statement)
1. [Hardware Set Up](#Hardware-Set-up)
1. [Writing Your Program](#Writing-Your-Program)
1. [Adding Blynk](#Adding-Blynk)
1. [Adding Alexa](#Adding-Alexa)

## Challenge Statement

Until the new high school is built, finding available parking at UAHS will be a challenge. You have been asked to build a proof-of-concept solution with the latest technology to help make parking easier. Your challenge is: *build a model parking lot with parking sensors to help drivers find open parking spots.* 

Your solution will involve hardware, software, and cloud solution components. A simple curcuit will detect the presence of cars in parking spots in a model parking lot. The Raspberry Pi or Arduino will turn LED lights on or off based on the sensor data using a program you'll write. Then, with Blynk, you'll be able to see the parking lot status on your phone. Finally (if you get this far!) you'll use Alexa with Blynk to ask how many spots are available. 

## Hardware Set Up

You will choose to use either the Arduino micocontroller or the Raspberry Pi 0 mini computer as the 'brain' of your solution. If you are not sure which to choose, we recommend choosing the Raspberry Pi. 

### Raspberry Pi 0
For the below steps you will be writing in files on the root of a linux file system as interpreted by windows. Rasbian picks up these files when it boots.  **When editing these files, make sure you use 'lf' line endings as opposed to 'crlf'**.  If you use VSCode you will see this as a drop down in the bottom right hand corner of the editor.  Other editors have similar options.
 
#### Flashing the SD Card
Follow the instructions on [this page](https://styxit.com/2017/03/14/headless-raspberry-setup.html) to get the OS loaded.  
* When you are downloading the OS, choose **Rasbian Lite**. 

#### Configuring the Boot Partition
* Per the article above, you will need to set up a wifi connection and place a marker file to start an ssh server. Here is a sample `wpa_supplicant.conf` file: 

```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=US

network={
    ssid="ssid"
    psk="password"
    key_mgmt=WPA-PSK
}
```

#### Remoting into the Pi via Wifi

* Put the SD card in the Pi Zero and power the Pi on. 
* Work with your coach and the on-site admin to determine the IP address of your Pi. 
* On the laptop, run the command `ssh pi@{pi ip address}` to connect. 
* The password will be `raspberry`. 

### Arduino

* Download Arduino IDE https://www.arduino.cc/en/main/software 
* Verify sample in IDE to configure set up using tutorial on site. 

## Writing Your Program

You may either write your program using Python or Java. Configuring the circuit support on the Pi with Java is a bit more complicated and involves building a tool from source. 

### Python
[Python Tutorial](https://raspberrypihq.com/making-a-led-blink-using-the-raspberry-pi-and-python/)

### Java (Harder setup)
[Java Instructions](java.md)

## Adding Blynk

Blynk allows your Pi or Arduino to send the state of the circuit to The Cloud. From there, you can access it on your phone in the Blynk App, and integrate Amazon Alexa.  

* Install the Blynk App on your phone. 

### Resources

[Blynk Intro Guide](http://docs.blynk.cc/#intro) – Provides basics of what Blynk is, how to setup an account, and how to build a new project.  You can stop at the “Getting started with Hardware” section. 

[Blynk API Info on Apiary](https://blynkapi.docs.apiary.io/#) - Provides an interactive interface to make api calls against Blynk.  Once you’ve created an account, and obtained an auth token, you can test functionality here

## Adding Alexa

You will build the capability to ask Alexa how many spots are open in the parking lot. 

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

1. Log in to [Amazon Alexa Developer Portal](http://developer.amazon.com/alexa). Username: `uahslearnathon@gmail.com` password: (ask a coach)
1. Scroll down and click `create a skill` button. 
1. Click the `start a skill` button. 
1. Click `create skill` button. 
1. Name the skill `TeamXSkill` with the team's name or number as X. Leave `custom` and `provision your own settings`. Click next.
1. Select `Fact skill` template. 
1. On the left menu, select `endpoint`. 
1. Add the ARN from the lambda in the default region box and hit `Save Endpoints` in the top left. 

### Calling Blynk from the Lambda

Modify the fact skill in the Amazon Developer portal and in the AWS lambda to call the Blynk API. 

### Testing The Skill

In the Alexa Developer Console, select the `Test` tab at the top. 

You can test in your browser using the Alexa Simulator. Use the microphone button to talk to Alexa to test the skill, or type a user's words into the box on the left.

To test on the device, ensure that `Skill testing is enabled in` is set to `Development`. 
