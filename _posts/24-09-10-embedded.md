---
layout: post
title:  "How I Got Into Embedded Systems and Practical Robotics"
categories: [Projects, ]
tags: []
image:
  path: 
  alt: 
---
> ## What I Learned In This Project
{: .prompt-tip}

## Why I Wanted To

As may be clear from other posts on this website, I love programming. I discovered this passion during my studies and especially during my Formula Student times. I discovered that this passion is especially focussed on autonomous systems, rather than web or app development. 

When I started down the path of autonomous systems engineering, and still today, the main focus of my engineering journey has been software in the area of guidance and navigation, along with some computer vision. This came about when I joined the driverless software team of the Ecurie Aix Formula Student team. 

I joined at the same time as a good friend of mine, and he went the more "logical" electrical engineering route, and became, well, an electrical engineer in the same team. Why is this the more logical route? My background explains why. I am, at heart, an electrical engineer. I started studying electrical engineering at RWTH Aachen University in 2016. 

And while I have absolutely found my place in the guidance and navigation area of autonomous systems, there has always been a part of me that was being pulled towards lower level electrical engineering and embedded systems engineering, which of course represented a large part of my studies. I find that understanding the foundations of how the software that I write works on a very low level makes everything seem like __sliiightly__ less black magic to me.

Therefore, I also believe that having at least a basic practical understanding of circuits, sensors, microcontrollers and hardware in general is essential for the autonomous systems engineer that I aspire to become, as these often comprise the very foundation of what the autonomous system will be running on. And it's also just highly interesting. Who doesn't want to build cool robots that drive around the apartment?

## Finally Starting My Embedded Journey

So now I have finally gotten around to it. It has taken only eight years. But rather late than never, right? Come along, and I will share what I learned. Maybe I can help smoothen your path a little while I'm at it.

## My First Project - A Self-Balancing Robot

Now, of course, being someone that is most intrigued by systems that do things by themselves (i.e. autonomous systems), I didn't just want to build a remote controlled robot. I saw the opportunity to get some practical experience on the mystical and crucial topic that is control. Something I have spent (and will still spend) months intensively studying for on paper during my studies, but have never actually used in a practical sense. 

So I decided that my very first project should be a **self-balancing robot**. 

When I started googling how to actually build a self balancing robot, I was hoping to find some tutorials or some explanations on how to do so. And while there were a few, those that I found were mainly just instructions, no real explanation of why what cable goes where and how to actually design such a device. While that may have worked, simply blindly following instructions was absolutely not what what I was looking for. Additionally, there where lists of what parts to buy for the project, and I regularly either didn't find the exact parts or wasn't certain if the parts I did find would actually work together. Furthermore, I still had an Arduino starter kit lying around that I had bought with the same thoughts of learning embedded programming five years earlier and had never touched. And I saw so many different types of self-balancing robots, that I decided: If they can build one without a tutorial, why can't I? Apart from the fact that I have almost no hardware or embedded experience at this point. But I wasn't going to let that stop me. I'll use what I have and order anything I need. 

That's what I did. I took a rough look at some of the tutorials to find out what items were essential to get started and go from there. Here's what I got with the first shipment:

1. [2x 6V geared DC motors, including wheels (Joy-It COM MOTOR03)](https://www.reichelt.de/mini-metallgetriebemotor-inkl-rad-und-halter-com-motor03-p258664.html)
2. [1x 3 axis gyroscope and 3 axis accelerometer (DEBO SENS 3AXIS, GY-521 board, MPU 6050 chip)](https://www.reichelt.de/entwicklerboards-beschleunigung-gyroskop-3-achsen-mpu-6050-debo-sens-3axis-p253987.html?&trstct=pos_0&nbc=1)
3. [1x on/off switch (Goobay 10013)](https://www.reichelt.de/miniatur-kippschalter-ein-aus-3-a-125-v-goobay-10013-p359360.html?&trstct=pos_0&nbc=1)
4. [1x 2 channel DC motor driver (DRV8833)](https://www.roboter-bausatz.de/p/2-kanal-drv8833-dc-motor-treiber-modul-3v-10v-1.5a-h-bruecke)
5. [2x DC-DC step up (XL6009)](https://www.roboter-bausatz.de/p/spannungswandler-xl6009-dc-dc-step-up-modul)
6. [Some jumper wires](https://www.roboter-bausatz.de/p/jumperkabel-sortiment-mit-verzinnten-enden-130-stueck)

At the point of writing this, I do not know if the parts will work together, nor do I know what parts I am missing. I looked at the specs, voltages, currents etc., and to my theoretical electrical engineering mind, they make sense, so lets see! Keep reading (especially if you are following along) to find out 😎.

For the sake of our collective learning, I will now provide a more detailed description of each of the parts. 

### Geared DC Motor

As the name implies, this is a DC motor that is geared. The gears reduce the motor's speed and therefore increase its torque. This is necessary to make small and strong adjustments that the robot need to keep its balance, especially considering the weight of all the components it carries. A slower motor also allows for finer, more precise control. 

This particular motor needs a 6V supply voltage and 160mA of supply current, and can achieve 300rpm. 

### IMU

Needed to sense the movement of the robot. The actual sensing is done by the MPU 6050 chip, which is a MEMS device (micro-electro-mechanical-system) containing a 3 axis gyroscope and a 3 axis accelerometer. It is housed on the GY-521 breakout board, which provides an interface to the chip for jumper wires and voltage regulation, among other things. It is a generic board design that is manufactured by DEBO SENS in my case.

### On/Off Switch

On/Off switch. Nuff said.

### 2 Channel DC Motor Driver

The DRV8833 acts as the interface between the Arduino and the 2 motors. It controls their speed, direction and torque. It amplifies the low-power control systems of the Arduino to provide the power to drive the motors. It contains two NMOS H-bridge drivers. Due to the fact that the drivers are constructed of MOSFET transistors instead of bipolar junction transistors (BJTs), they are  more efficient than BJT based drivers. At least on paper, I don't have any practical experience to back that.

### DC-DC Step Up

Increases one DC voltage to a higher one. I saw that this was needed in a tutorial and I am not yet sure when exactly I will need it. If you are just as interested as me, keep reading! I never thought I would write a detective story, but here we are 🕵️. 

### Jumper Wires

Unfortunately, motors powered by bluetooth don't exist yet.

## Step 1: Controlling DC Motors With the Motor Drivers

https://lastminuteengineers.com/drv8833-arduino-tutorial/