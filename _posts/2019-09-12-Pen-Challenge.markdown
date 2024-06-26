---
layout: post
read_time: false
show_date: false
title: "Sindelar - Robotic Pen Locator"
# date: 2019-09-12
img: "posts/Pen_Challenge/pen_cover_new.png"
# tags: [OpenCV, Python]
category: opinion
author: Meg Sindelar
description: "Implemented a realsense camera using OpenCV to communicate to a robotic arm where a purple pen is in space, and have the robotic arm move to and grab the pen."
---
The goal of this project was to locate a purple pen in space using OpenCV and grab it with a robotic arm.


<video width="720" height="480" controls="controls">
  <source src="https://user-images.githubusercontent.com/87098227/207751323-f2737d6e-292a-421c-9dd6-27d78a489c69.mp4" type="video/mp4">
</video>

Software: OpenCV, Python

Hardware: PincherX 100, Intel Realsense D435i

Using a realsense camera, I implemented computer vision techniques to identify the centroid purple pen by aligning the RGB image with the depth map. I identified the purple color of the pen by specifying the RGB threshold pixels to detect, and then used edge detection to find the outline of the pen. From their, I could easily find the centroid. I then read in the data of the centroid and depth from the realsense and transformed the frame from the realsense camera to the end-effector of the robot to determine how to move the robot. Based on these calculations, I incremented the joint angles of the robot to move the end-effector of the arm to the centroid of the purple pen and then grasp the pen.
