---
layout: post
read_time: true
show_date: true
title: "Software of a Novel Multi-Metal 3D Printer"
date: 2021-03-24
img: 
tags: [general blogging, thoughts, life]
author: Meg Sindear
description:
---
The goal of this project was to create the software for an initial prototype of a novel multi-metal 3D printer to create completely 3D-printed electric motors. Unfortunately, this invention is still under development, so I cannot expand into too many details or show images of the prototype itself.

"Image"

Software: B&amp;R Automation Studio Ladder Logic, C

Hardware: B&amp;R CPU, stepper motors, limit switches, digital I/O modules, augers, piezo electrics

The project was split up into a few diffrent teams, where I was the sole individual on the software development team. I designed a control system architecture using ladder logic and C programming on a B&amp;R PLC platform. The architecture of the code consisted of multiple conditional-based state machines used to control the stepper motors of the build plate, the powder augers, and limit switch conditions.


I also worked with the mechanical design team to test and debug the powder mixing and distribution chamber, which utilized multiple augers and piezo electrics to control the powder flow.

Additionally, to allow the mechanical design team to test multiple parts with my software, I created a simple HMI user interface with documentation. The interface allowed the user to specify different control parameters and to see how their parts functioned within the rest of the working system.

Overall, my part of the project was a success, where I implemented ___ in time for the initial proof of concept prototype deadline.

The 3D printer is an invention of the (post doc) Buzz ____ from UW-Madison. 