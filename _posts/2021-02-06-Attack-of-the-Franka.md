---
layout: post
read_time: true
show_date: true
title: "Attack of the Franka"
date: 2021-01-06 #2021-01 - 2021-06
img: "posts/20210206/Attack_of_the_Franka.jpg"
#tags: [neural networks, machine learning, artificial intelligence]
#category: 
author: Meg Sindelar
description: 
---
The goal of this project was to configure a robot to autonomously wield a lightsaber to knock down enemies, represented by red blocks, without knocking down its allies, represented by blue blocks.

<video width="720" height="480" controls="controls">
  <source src="https://user-images.githubusercontent.com/113186159/206842696-c61fa77b-1fb3-462e-9ac9-2ade4ed72283.mp4" type="video/mp4">
</video>

Software: Python, ROS2, MoveIt, OpenCV, RVIZ

Hardware: 7 DOF Franka Emika Panda, RealSense D435i camera, 

I worked on this project in a team of 4, with my other team members including Nick Morales, Vaishnavi Dornadula, and Sushma Chandra. This project was split into computer vision and motion planning, where I focused on the motion planning side.


Overall, the system detects the difference between the blue and red blocks through OpenCV color detection tecniques. The colors are determined from the RGB image with the use of HSV threshold to draw contours. Additionally, depth filters are utilizeds to find transforms relative to the base of the robot. These are then passed into our motion planning ROS2 node. Images of the color detection and the transformations is shown below.

<center><img src='./assets/img/posts/20210206/Camera_CV.png' width="540"></center><br>
<center><img src='./assets/img/posts/20210206/RVIZ_CV.png' width="540"></center><br>

As for the motion, first the robot starts by picking up the lightsaber from a 3D-printed stand. In order to accomplish this, the lightsaber is first added as a collision object in the MoveIt planning scene, then the robot moves towards the lightsaber through specific end-effector poses. Then, the lightsaber gets removed from the scene as a collision object, the robot graps the lightsaber, and the lightsaber is added as an attached collision object.

Next, the robot begins to destroy its enemies by looking to the leftmost enemy first. Depending on where the allies are in the environment, which get added to the MoveIt planning scene as collision objects, the robot decides which of 3 path planning options to take. Two of its options are left and right swings, both commanded by end-effector waypoint poses. These poses are determined by the locations detected through the transforms from the camera node from computer vision. The last motion planning option is a stabbing motion, which is commanded through a combination of the position of the enemy and set joint position ranges. The decision sequence works by first attempting to plan a left swing, then a right swing, and then a stabbing motion. The robot makes this decision based on where the allies are in the scene and if it can knock over the enemy block without knocking over any ally blocks. If the robot decides it cannot knock over an enemy block without knocking over any allies, then it will move onto the next one. The robot will continue to perform this decision sequence until all the reachable enemies have been knocked down. An image of the MoveIt RVIZ planning scene can be scene below.

<center><img src='./assets/img/posts/20210206/Planning_Scene.png' width="540"></center><br>
