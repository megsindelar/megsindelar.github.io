---
layout: post
read_time: false
show_date: false
title: "Sindelar - Active SLAM"
# date: 2021-01-06 #2021-01 - 2021-06
# img: posts/Header/drift_parking_car.gif
# tags: [C++, OpenCV]
# category: 
author: Meg Sindelar
description: 
---
The goal of this project was to create an active pose-graph SLAM architecture using visual measurements on a physical system to maneuver around a poster board and be able 
to localize and recreate a map of the environment. There is a large focus on the visual search of this project.

** video here **

Software: C++, OpenCV, SESync, Sophus, Eigen, TEASER

Hardware: Turtlebot3, Raspberry Pi, Raspberry Pi Cam V2, OpenCR board, RGB LEDS

Github link: [Github](https://github.com/megsindelar/active_slam)

Below is a block diagram for the entire active SLAM system:

![block_diag_active_slam](https://github.com/megsindelar/megsindelar.github.io/assets/87098227/20f29036-a69e-4564-8f3f-12e351322b8d)

In this system, the camera is mounted on the turtlebot so that it is only ___ meters from the ground, therefore limiting its field of view to a very small area. The point of this is to rely more on the image registration and decision making processes to try to prove robustness of those systems.

For my SLAM system I use estimated turtlebot poses based on wheel encoder odometry and visual measurements for loop closure to update the graph. I utilize the SE-Sync system to update each node position based on individual information matrices, where I configure them to rely more on the visual loop closure measurements than the wheel odometry.

One challenge with creating this project on a real-world physical system is due to hardware limitations. The wheel odometry is never perfectly accuate due to wheel slippage and/or the wheels getting stuck on small bumps on the floor. Additionally, due to the limited resolution of the Raspberry Pi camera, the image registration metrics and additional tests of odom distance and OpenCV matches distances would vary from test to test, therefore making it unreasonable to try to threshold these tests to allow enough real loop closures while blocking out all false loop closures. Thus, it was decided to instead pivot to computing the mean-squared error between images nearby the designated looping node and use the best image and location from that test as a loop.  

The decision making process currently consists of ... The Phd student I was working with will next use my system to implement his ergodic metric algorithm for the decision making part of this system.





