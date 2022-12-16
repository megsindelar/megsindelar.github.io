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

The feedback contoller outputs a twist which is then used, in combination with the pseudoinverse of the end-effector Jacobian, to find the wheel and arm joint speeds.

These new speeds are used to calculate the next state the robot is in at the next time step. The importance of a well-tuned feedforward plus PI controller can be seen in the error graphs below, where the overshoot graph many rapid oscillations. This means that the robot would initially exhibit crazy, and in real life dangerous, motions as it tried to get back on track to its desired trajectory.

Well-tuned feedforward plus PI feedback controller



Overshoot due to a poorly-tuned feedforward plus PI feedback controller


To make the robot more realistic, I also implemented joint limits on 4 of the 5 arm joints. I chose only the first 4 out of the total 5 joints to constrain because in the desired trajectory I command a specific position for joint 5. Therefore, a constraint on joint 5 seemed to be an unnecessary addition that would overconstrain the problem. Adding the joint constraints forces the robot to plan trajectories to pick and place the block without any self-collisions or singularities. This process works by first planning the robot configuration at the next time step without executing. Then, the four specified joints are check to see if they remain between the upper and lower bounds of the limits. If not, the column of the Jacobian matrix corresponding to that joint is set to all zeros. This suggests to the controls that moving that specific joint won't cause any end-effector motion, thus the new controls won't command any motion for that specific joint. The difference between not having joint limits and implementing them are respectively shown below. 

Example of a tuned feedforward plus PI feedback controller without joint limits.
<video width="720" height="480" controls="controls">
  <source src="https://user-images.githubusercontent.com/113186159/206842696-c61fa77b-1fb3-462e-9ac9-2ade4ed72283.mp4" type="video/mp4">
</video>



Example of a tuned feedforward plus PI feedback controller with joint limits.
<video width="720" height="480" controls="controls">
  <source src="https://user-images.githubusercontent.com/113186159/206842696-c61fa77b-1fb3-462e-9ac9-2ade4ed72283.mp4" type="video/mp4">
</video>