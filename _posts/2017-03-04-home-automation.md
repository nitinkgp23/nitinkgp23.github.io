---
title: Home automation
#description: Using arduino to remotely control tubelights and fans through a smartphone.
date: 2017-03-04
categories:
 - tutorial
tags:
 - arduino
 - automation
comments: true
---



Lying on the bed, just before dozing off to sleep every night, I wondered how wonderful it would be if my roomie would get up from his bed and switch off the tubelight for me. Ohh, throwing all sort of tantrums and tempting offers to my roomies to make them get up from bed for me was hell of a job. Sometimes I would succeed, but mostly, I would have to get out from the quilt, in shivering cold, and trouble my legs to walk a 3 metre distance to turn off the switch.
<!-- more -->
And then, I came across this wonderful thing called Arduino. A bit of googling, and I was ready to automate my tubelights and fans, so that I would control them from my mobile phone itself. No more tantrums and no more trouble to my legs. I was glad.

Here is a detailed explanation of what I used, and the steps required to automate your room!

## Required

* Arduino UNO  (Purchase here)
* Bluetooth Module (Purchase here)
* Breadboard / PCB board
* Wires , Jumper wires
* 12 V relay (1 relay for each device you want to control)
* 12 V adapter
* TIP 122 transistor
* Android phone

This blog won’t explain the theoretical reasons behind each of the steps, or the working of Arduino or anything that is of no use in the project. It just serves as a guide to the steps you need to follow, to build a home automated system. A little knowledge about how circuits work will suffice.

This is an Arduino UNO board. There are 14 digital I/O pins, and 6 analog inputs, 3 GND pins, a 3.3 V and a 5 V pin. We will be using pin 13 for controlling the appliance, pin 1 and pin 0 will be used for connecting to the bluetooth module, and 5 V pin will be used to power the bluetooth module. GND pins will be used for connecting to the ground.

![Arduino](https://github.com/nitinkgp23/nitinkgp23.github.io/blob/master/assets/images/posts/home-automation/48912-arduinouno_r3_front.jpg)

This is HC-05 bluetooth module, which will be used for communicating through the mobile device. It will have the usual range of 10 m, but if you want to have a higher range, you can look at other modules available online.

![HC-05 bluetooth module](https://github.com/nitinkgp23/nitinkgp23.github.io/blob/master/assets/images/posts/home-automation/134883010_14170929051_large1.jpg)

The module that you have bought might consist of 6 pins, but we will be using only 4 pins that lie in the middle, labelled VCC, GND, TX and RX. An important thing to note here is that, TX pins have to be connected at 3.3 V Level, whereas the power required in the bluetooth module is 3.6-6 V. Hence, we have to use the 5 V pin from the arduino to power the module, and divide the voltage and drop it down to 3.3 V, so that bluetooth module doesn’t get cooked up.

Here is how a connection should be made between arduino and the bluetooth module :

![Connecting arduino and bluetooth](https://github.com/nitinkgp23/nitinkgp23.github.io/blob/master/assets/images/posts/home-automation/134883010_14170929051_large1.jpg)

#### Points to be noted:

RX pin of the module connects to TX pin of the arduino and vice-versa.
TX pin of the module works at not more than 3.3 V level, hence a voltage-divider circuit is used, where 1/3 * 5 V goes to the GND, whereas only 2/3 * 5 V is used up in the RX pin of the arduino.
Connect GND of the module to any of the GND pins on the arduino board.
Connect VCC of the module to 5 V pin of the arduino board.
Controlling a LED by bluetooth:

![](https://github.com/nitinkgp23/nitinkgp23.github.io/blob/master/assets/images/posts/home-automation/screenshot-from-2017-01-17-17-09-55.jpg)

Make the above connection. The above diagram only shows how to make the connection. You are free to connect the LED and wires through PCB board or breadboard. Use a proper resistor according to the LED you are using.

A 220 ohm resistor for a red LED will be okay, if you are connecting the arduino by USB,

#### Uploading the code to Arduino board :

First of all, download Arduino IDE from here. Follow the instructions and install the IDE. Connect the arduino board to computer, and upload the following code to the board. Google a bit on how to use the Arduino IDE, and how to upload a code. While uploading, make sure you have disconnected the RX and TX pins from the bluetooth module, otherwise an error will flash up. After the code has uploaded successfully, reconnect the RX and TX pins.

#### Downloading the app from play store :

Download [this](https://play.google.com/store/apps/details?id=com.app.control&hl=en) app from Google Play Store (Arduino bluetooth control , by Guiming Apps), and install it in your android phone.
