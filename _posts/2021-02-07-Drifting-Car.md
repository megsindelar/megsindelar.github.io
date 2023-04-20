---
layout: post
read_time: false
show_date: false
title: "Sindelar - Autonomous Drift Parking"
# date: 2021-01-06 #2021-01 - 2021-06
img: posts/Header/drift_parking_car.gif
# tags: [C++]
# category: 
author: Meg Sindelar
description: 
---
The goal of this project was to create a drifing car that could autonomously powerslide into a parallel parking spot.

{% include youtube.html id="_rUVOUsGAXA" %}

Software: C++

Hardware: Brushless DC motor, VESC, Jeston Nano, Servo, PIC32, Arduino

Github link: [Github](https://github.com/megsindelar/autonomous-drift-parking-car)

For my system I created a feedforward PI controller in a multi-threaded C++ program to read feedback from steer and throttle encoders. The controller follows multiple different reference trajectories to slide into the parking spot.

The vehicle is a 4WD RC car, which normally is more difficult to make drift than a RWD car. Therefore, to make the car drift, I put pvc pipe on the two front wheels. This helps the car slide into the spot when it turns.

![IMG-0392](https://user-images.githubusercontent.com/87098227/226077342-5ff8e98f-e626-40f4-a14c-fd39bacd15a4.jpg)

Additionally, to upgrade the RC car, I created an entirely new circuit diagram, as seen below.

![Screenshot from 2023-03-31 02-03-43](https://user-images.githubusercontent.com/87098227/229047503-eb8d83ae-de90-4df5-9763-acbf0cb996ba.png)

For this system, the Jetson Nano is my main module that communicates with other modules to control the car. For the throttle, I opened the PWM ports on the Jetson Nano using direct memory access to send the signal to the VESC to control the brushless DC motor. Then, for the steer, I connected an Arduino to the Jetson Nano and used serial communication to send commands to the Arduino to control the servo for steering. Next, there are two Raspberry Picos that are used as quadrature converters to read both the throttle and steer encoders. I also use serial communication to read the encoder data. 

Below is my block diagram for my controller:
![Screenshot from 2023-04-02 13-05-33](https://user-images.githubusercontent.com/87098227/229370685-4fe9fc79-ab39-49c6-ae7e-8e8676e74d78.png)


**Future Work:**
I have two ideas for different ML algorithms to implement on this vehicle as a better control system to drift into a parallel parking spot.

1. Implement this open-source SAC-based algorithm, [1], to have the car learn to drift which it then can learn to slide into the parking spot. For this, I have already extracted the machine learning model from the simulator and modeled the kinematics of the car by representing the two sliding wheels (the ones with pvc pipe) as mechanum wheels, where the angle of the ackermann steering car affects the angle of the rollers on the mechanum wheels. This modeling technique would be used instead of trying to model the car with friction as it is still an unsolved problem and very difficult to estimate. I also implemented a neural network to estimate the slip velocity based on feedback data from my specific vehicle. 

2. Develop a real-time ML algorithm that is based on the Koopman operator to use as the controller of the car. The model would consist of getting world positions from a high-speed camera viewing the environment from above and update the controls of the system based on its position. This type of algorithm has also been tested on other models that cannot be simulated and have very good success.



**References:**

[1]  @article{Cai2020HighSpeedAD,
  title={High-Speed Autonomous Drifting With Deep Reinforcement Learning},
  author={Peide Cai and X. Mei and L. Tai and Yuxiang Sun and M. Liu},
  journal={IEEE Robotics and Automation Letters},
  year={2020},
  volume={5},
  pages={1247-1254}
}
