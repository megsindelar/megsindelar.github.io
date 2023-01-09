---
layout: post
read_time: true
show_date: false 
title: "Software of a Novel Multi-Metal 3D Printer"
# date: 2020-03-24 #2021-03-24
img: posts/Software_Invention/metal_3d_printing.png
tags: [Software Architecture, Ladder Logic, C, 3D-printing]
author: Meg Sindear
description:
---
The goal of this project was to create the software for an initial prototype of a novel multi-metal 3D printer to create completely 3D-printed electric motors.

Unfortunately, this invention is still under development, so I cannot expand into too many details or show images of the prototype itself.


Software: B&amp;R Automation Studio Ladder Logic, C

Hardware: B&amp;R CPU, stepper motors, limit switches, digital I/O modules, augers, piezo electrics

The project was split up into a few diffrent teams, where I was the sole individual on the software development team. I designed a control system architecture using ladder logic and C programming on a B&amp;R PLC platform. The architecture of the code consisted of multiple conditional-based state machines used to control the stepper motors of the build plate, the powder augers, and limit switch conditions.


I also worked with the mechanical design team to test and debug the powder mixing and distribution chamber, which utilized multiple augers and piezo electrics to control the powder flow. Below is a diagram of the subsections of components I configured and systems I created.

![Screenshot from 2023-01-09 10-47-57](https://user-images.githubusercontent.com/87098227/211362197-64e34986-7830-4ebb-aacb-754b48de0a33.png)

Additionally, to allow the mechanical design team to test multiple parts with my software, I created a simple HMI user interface with documentation. The interface allowed the user to specify different control parameters and to see how their parts functioned within the rest of the working system.

Overall, my part of the project was a success, where I implemented a software system for the initial proof of concept in time for the prototype deadline.

This multi-metal 3D-printer is an invention of the co-founder and CEO of Dastan Technologies, Behzad “Buzz” Rankouhi, from UW-Madison. 
