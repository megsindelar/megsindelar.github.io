---
layout: post
read_time: true
show_date: true
title: "Robot Manipulation"
# date: 2021-01-06 #2021-01 - 2021-06
img: "posts/Attack_of_the_Franka/Attack_of_the_Franka.png"
#tags: [neural networks, machine learning, artificial intelligence]
#category: 
author: Meg Sindelar
description: 
---
The goal of this project was to implement a feedforward plus PI feedback controller, based on calculated odometry, for a simulated mobile Kuka youBot robot to follow a generated pick and place trajectory.

<video width="720" height="480" controls="controls">
  <source src="https://user-images.githubusercontent.com/113186159/206842696-c61fa77b-1fb3-462e-9ac9-2ade4ed72283.mp4" type="video/mp4">
</video>

Software: Python, CoppeliaSim

There were three steps to this project. First, I generated a desired end-effector trajectory to pick and place a block. Next, I then determined the robot chassis configuation, based on its odometry, and the arm configuration, from first-order Euler Integration, at each time step. Finally, I then implemented a feedforward plus PI feedback controller to correct the robots path if it deviates from the desired generated trajectory. The model of my feedforward plus PI feedback controller is shown below.

"math here"

Additionally, to make the robot more realistic, I implemented joint limits to 4 of the 5 arm joints. I chose only 4 out of the 5 joints to constrain because in my trajectory I command a specific position for joint 5, so it seemed to be an unnecessary addition that would overconstrain the problem.