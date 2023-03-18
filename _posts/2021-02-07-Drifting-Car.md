---
layout: post
read_time: true
show_date: false
title: "Autonomous Parallel Parking Drift Car"
# date: 2021-01-06 #2021-01 - 2021-06
img: posts/Header/drift_parking.gif
tags: [C++]
# category: 
author: Meg Sindelar
description: 
---
The goal of this project was to create a drifing car that could autonomously powerslide into a parallel parking spot.

<video src="https://user-images.githubusercontent.com/87098227/226077785-7c41633c-0b24-44a4-a2bb-61c67c5146b3.mp4" controls="controls" style="max-width: 730px;">
</video>

Software: C++

Hardware: Brushless DC motor, VESC, Jeston Nano, Servo, PIC32, Arduino

Github link: <a href="(https://github.com/megsindelar/autonomous-drift-parking-car)"> https://github.com/megsindelar/autonomous-drift-parking-car </a>


For my system I created a feedforward PI controller in a multi-threaded C++ program to read feedback from steer and throttle encoders. The controller follows multiple different reference trajectories to slide into the parking spot.

The vehicle is a 4WD RC car, which normally is more difficult to make drift than a RWD car. Therefore, to make the car drift, I put pvc pipe on the two front wheels. This helps the car slide into the spot when it turns.

![IMG-0392](https://user-images.githubusercontent.com/87098227/226077342-5ff8e98f-e626-40f4-a14c-fd39bacd15a4.jpg)

Additionally, to upgrade the RC car, I created an entirely new circuit diagram, as seen below.

![car_circuit_diagram](https://user-images.githubusercontent.com/87098227/226084838-14ad9e0b-c22f-40e6-8ca4-77f9c1a1572c.png)

For this system, the Jetson Nano is my main module that communicates with other modules to control the car. For the throttle, I opened the PWM ports on the Jetson Nano using direct memory access to send the signal to the VESC to control the brushless DC motor. Then, for the steer, I connected an Arduino to the Jetson Nano and used serial communication to send commands to the Arduino to control the servo for steering. Next, there are two PIC32's that are used as quadrature converters to read both the throttle and steer encoders. I also use serial communication to read the encoder data. 

Below are two more trajectories of the car sliding into a parking spot:

https://user-images.githubusercontent.com/87098227/226085126-b6397616-634d-4579-a8b6-12d43efa1120.mp4




https://user-images.githubusercontent.com/87098227/226085112-c1b7507b-579b-428f-8452-0de2543a2d5a.mp4


