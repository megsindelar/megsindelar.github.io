---
layout: post
read_time: true
show_date: true
title: "Robotic Pen Locator"
# date: 2019-09-12
img: 
tags: [copyright, creativity, neural networks, machine learning, artificial intelligence]
category: opinion
author: Meg Sindelar
description: "Implemented a realsense camera using OpenCV to communicate to a robotic arm where a purple pen is in space, and have the robotic arm move to and grab the pen."
---
The goal of this project was to locate a purple pen in space using OpenCV and grab it with a robotic arm.

[pen_locator.webm](https://user-images.githubusercontent.com/87098227/201566029-3bbd70ee-b4f7-40f7-b1ee-55b270418cfe.webm)

Software: OpenCV, Python

Hardware: PincherX 100, Intel Realsense D435i

Using a realsense camera, I implemented computer vision techniques to identify the centroid purple pen by aligning the RGB image with the depth map. I identified the purple color of the pen by specifying the RGB threshold pixels to detect, and then used edge detection to find the outline of the pen. From their, I could easily find the centroid. I then read in the data of the centroid and depth from the realsense and transformed the frame from the realsense camera to the end-effector of the robot to determine how to move the robot. Based on these calculations, I incremented the joint angles of the robot to move the end-effector of the arm to the centroid of the purple pen and then grasp the pen.
