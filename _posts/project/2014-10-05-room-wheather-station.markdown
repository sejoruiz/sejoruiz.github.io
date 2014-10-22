---
layout: project
title:  "Room Weather Station"
date:   2014-04-25 16:54:46
author: Sergio Ruiz
categories:
- project
- electronics
- arduino
tags:
- weather
- arduino
- electronics
- sensors
- meteo
- bootstrap
img: seasons.jpg
thumb: seasons.jpg
images_root: meteo
carousel:
- single01.jpg
- single02.jpg
- single03.jpg
website: http://sergioruiz.duckdns.org
---

###Room Weather Station

Since I moved to Sweden I had a small problem. I never knew which temperature my room was. While is not a big inconvenient, it is an opportunity for another small electronics project. When I started thinking about that, I recently acquired an Arduino MEGA board, and I thought I could make something out of that. With a couple of extra components, I would be able to monitor the temperature, light and humidity of my room. I could even put a couple of sensors outside of my apartment, and also monitor the outdoor weather. In other words, I wanted to build a weather station. So, one rainy weekend, I decided to start developing this project. As always, you can go to my GitHub and [fork the code](#) of the project. Here we go!


###1. Introduction: Requirements

The requirements of this project are related with all the sensors a weather station requires. All the sensor reading will be done through an Arduino board (it doesn't matter which model, but keep in mind all the code is designed for Arduino MEGA). The Arduino board will transmit these measures to the Raspberry Pi through the Serial interface. The sensors can be also read directly through the GPIO pins of the Raspberry, so the Arduino is optional. However, if the Arduino is not used, the measures will be less accurate. 


####1.1. General Requirements

I'm going to list first the requirements for the general system, and then, I'll introduce the particular requirements for each sensor. That way, you can build the station with as many sensors as you want. Let's get down to business. Here is the list of general requirements. The exact components I used are in brackets:

-	Raspberry Pi (Model B+)
-	Arduino board (Arduino MEGA2560)
-	1 Breadboard or other support for the circuit
-	Du-Pont lines and cables for making the connections
-	LCD Display (optional) in case we want to have a screen that shows the data
-	1 47nF Capacitor
-	USB cable for the Arduino board


####1.2. Light Sensor Requirements

Light sensors are usually a resistor that changes the value depending on the light. These kind of light sensors, often referred as photoresistors are an easy way of measuring light. If you are interested about them, you can have a look at its [Wikipedia article](http://en.wikipedia.org/wiki/Photoresistor). For the implementation of the light sensor circuit we will need:

-	1 Photoresistor
-	1 1M resistor. Please refer to the hardware assembly section for more details about the correct value for this resistor


####1.3. Temperature Sensor Requirements

In this application, we will use the temperature sensor LM-35. This component is already calibrated for ºC,  and it's enough precise for the requirements. 

-	1 LM-35 (I'm using LM-35DZ)
-	1 100K resistor (any resistor higher than 10K will do)


####1.4. Humidity Sensor Requirements

The humidity sensor is the sensor that will require more extra hardware. We have several choices here. The easiest one is to buy an Arduino shield that includes a humidity sensor. These shields come already calibrated, and they require almost no code to work. However, any failure in the sensor means that we need to acquire a new shield. On the other hand, one can buy a humidity sensor for a 10th of the price of the shield. These sensors are not calibrated, and are generally harder to use. However, any reparation is very cheap and easy to do. In this project, I have used this second option. We need the following components:

-	1 Humidity sensor (HCZ-D5-A)
-	2 270 ohms resistor.
-	3 47nF capacitors
-	1 100nF capacitor
-	2 4.7mH inductances
-	1 100K potenciometer.


###2. Assembling The Hardware

During this section, we will also follow the structure of the previous paragraphs. First, I describe the procedure for assembling the general hardware. Afterwards, the circuit for each particular sensor is explained. Here we go!


####2.1. General hardware

The general hardware shows how to connect the Raspberry with the Arduino, along with the breedboard. This initial setup have the 47nF placed between 5V and GND to stabilize the 5V output. It's a good practice to use it, although is not completely required. The Arduino is connected to the Raspberry Pi via USB interface. Finally, the 5V and GND are connected to the breadboard. At this point, it is highly recommendable to look [how a breadboard works](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard). In the following picture, you can have a look at the diagram of the circuit we are building.

<a href={{site.project_img}}{{page.images_root}}/generalcircuit.png rel="prettyPhoto" title="Assembling the general hardware"><img src={{site.project_img}}{{page.images_root}}/generalcircuit.png alt="Diagram of the general hardware circuit" /></a>


####2.2. Light sensor assembly

As mentioned previously, the light sensor is basically a ligh dependent resistor. We can guess the value of that resistor by connecting another resistor, and supply a known voltage. We want to use the 1.1V reference for higher precision. Thus, we need to find the appropriate value of the resistor that makes the voltage in the photoresistor vary between 1.1V and 0 when the supply voltage is 3.3V. For this purpose we can build the following "testing" circuit:

<a href={{site.project_img}}{{page.images_root}}/lightcircuit.png rel="prettyPhoto" title="Assembling the light sensor hardware"><img src={{site.project_img}}{{page.images_root}}/lightcircuit.png alt="Diagram of the light sensor hardware circuit" /></a>

In this circuit, we can then proceed to read the port A2 from the Arduino, and print the value via Serial. All of this is already done in the code on GitHub, so don't worry.
We need to perform a measure when the impedance (resistance) of the light sensor is higher. Light sensors typically increase their impedance when they receive less light. So all we need to do is to take a measure when it's as dark as possible. in my case, I took the measures with all the lights off and in the middle of the night. I obtained a measure of 190. Each point is equal to 5mV, so that means that in the worst case, the light dependent resistor is eating 0.95V from the total 3.3V. We are interested on keeping that max voltage under 1.1V. If the voltage is higher, we need to change the 1M resistor with something higher. As this wasn't my case, I didn't need to change the 1M resistor.


####2.3. Temperature sensor

The temperature sensor will work almost out of the box. Here you can find a suggestionon how to assemble the hardware. It's important to know that the LM35 is represented with the flat size LOOKING AT US. Please refer to the [datasheet of the LM35](http://www.ti.com.cn/cn/lit/ds/symlink/lm35.pdf) to make sure you are making the right connections. 

<a href={{site.project_img}}{{page.images_root}}/tempcircuit.png rel="prettyPhoto" title="Assembling the temperature sensor hardware"><img src={{site.project_img}}{{page.images_root}}/tempcircuit.png alt="Diagram of the temperature sensor hardware circuit" /></a>


###3. Conclusion

Now we have all the system assembled. We only need to load the software onto the board, and we will have our station running! So you just need to go to [GitHub](#) and download the code from there. Then you can load it using the Arduino IDE. Make sure you select the correct board! I'll be probably updating this post as soon as I implement more features, so stay tuned and don't forget to leave me a feedback! 

