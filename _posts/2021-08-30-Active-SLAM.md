---
layout: post
read_time: false
show_date: false
title: "Sindelar - Active SLAM"
# date: 2021-01-06 #2021-01 - 2021-06
img: posts/Header/active_slam_gif.gif
# tags: [C++, OpenCV]
# category: 
author: Meg Sindelar
description: 
---
The goal of this project was to create an active pose-graph SLAM architecture using visual measurements on a physical system to maneuver around a poster board and be able 
to localize and recreate a map of the environment. There is a large focus on the visual search of this project.

{% include youtube.html id="wC03MrdOM5E" %}

Software: C++, OpenCV, SESync, Sophus, Eigen, TEASER

Hardware: Turtlebot3, Raspberry Pi, Raspberry Pi Cam V2, OpenCR board, RGB LEDS

Github link: [Github](https://github.com/megsindelar/active_slam)

Below are images of the poster reconstruction before (left) and after (right) a loop closure.

![loop6_before_and_after](https://github.com/megsindelar/megsindelar.github.io/assets/87098227/9db6d80d-b079-4aa7-9fc4-ba63d1aa12a4)

Below is a block diagram for the entire active SLAM system:

![Screenshot from 2023-08-25 09-18-27](https://github.com/megsindelar/megsindelar.github.io/assets/87098227/63bfb8af-99f7-4373-95ef-4253298552fa)

In this system, the camera is mounted on the turtlebot so that it is only 0.7 meters from the ground, therefore limiting its field of view to a very small area. The point of this is to rely more on the image registration and decision making processes to try to prove robustness of those systems. Below are a few images of the turtlebot used.

![turtlebot](https://github.com/megsindelar/megsindelar.github.io/assets/87098227/fd942c39-36b9-4c6b-9706-eef5262b00e8)

For my SLAM system I use estimated turtlebot poses based on wheel encoder odometry and visual measurements for loop closure to update the graph. I utilize the SE-Sync system to update each node position based on individual information matrices, where I configure them to rely more on the visual loop closure measurements than the wheel odometry.

The decision making process currently consists of waypoint planning with loops triggered every specific number of nodes. When the turtlebot reaches the desired loop-back node, the turtlebot performs a local visual search for the real loop.  The Phd student I was working with will next use my system to implement his ergodic metric algorithm for the decision making part of this system.


**Decision behind visual search**

Originally, instead of a visual search, I had three tests to try to verify if the loop closure was a real loop or a false positive. 

In graph-based SLAM, it is crucial to not let any false positive loops through, because while loop closures help to update and optimize the graph, a false positive completely messes the graph up and hurts the graph a lot more than a true positive helps. My tests for this problem included utilizing bag of words within a circular region around the turtlebot, along with then comparing top candidates to odom distances and OpenCV matcher distances.

However, due to hardware limitations, this combination of tests was unreliable. I tried making all the tests as strict as possible, however not enough loops were detected and the wheel odometry went uncorrected for too long. But, if I made some of the tests a little more lenient, it would lead to too many inaccurate false positives.

First off, the wheel odometry would suffer from wheel slippage, getting stuck on small bumps, such as dirt and pebbles tracked in, on the floor, and getting stuck if the turtlebot went off the poster and attempted to get back on. The error would greatly accumulate over time if the graph was built with too many nodes and not enough true positive loop closures.

The visual measurements are supposed to come into play to offset the wheel odom issues. However, due to hardware limitations there too, image registration techniques only worked so well. The Raspberry Pi camera has limited resolution for each frame, which led to the image registration bag of words metrics and OpenCV matches distances values varying greatly in identical tests. It became unreasonable to try to threshold these in combination with the wheel odometry. 

Therefore, it was decided to instead pivot to a local visual search technique. A diagram of the idea of the visual search can be seend below.

![Visual_Search_](https://github.com/megsindelar/megsindelar.github.io/assets/87098227/0c8454b9-6864-410e-bf8e-812292ed3472)

During this search, the mean-squared error would be computed between the loop node image and each scan node image. The best image and location from that test was used as a loop. This method proved to be good for a small loop, however this method would still allow false positives when the uncertainty in wheel odometry would become too high. 

The focus of the project became weighted more on the visual search technique to demonstrate a comparison and proof of concept loops.


**Future improvements**

If I had more time, I would maybe try to combine the local visual search MSE with bag of words and then increase the desire for more visual searches. Finding more true positive loops would help the turtlebot to continually update its odometry so it doesn't veer off too much.






