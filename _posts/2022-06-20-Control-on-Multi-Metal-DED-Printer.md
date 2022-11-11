---
layout: post
read_time: true
show_date: true
title: "Feedback Control on a Multi-Metal DED Printer"
date: 2021-04-02
img: 
tags: [neural networks, machine learning, artificial intelligence]
category: theory
author: Meg Sindelar
description: 
---
The goal of this project was to design and implement a signature-based feedback control system on a LENS Multi-Metal DED Printer.
"Image"
  

This was my project as a Research Assistant at the University of Wisconsin-Madison. There were three overall stages, the first of which I was tasked with. My stage was to create a feedback control system for the build height of a print, both in-situ and ex-situ, as an initial proof of concept. I was the sole individual on this part of the project. The system layout for the project is shown below.

![Screenshot from 2022-11-10 20-16-17](https://user-images.githubusercontent.com/87098227/201249031-e765f638-ebf7-45ba-a9aa-75ef26c3d1a6.png)

This first project staged contained three main parts, including software integration, measurement equipment, and the control system. 

**Software Integration:**

This was the biggest part of my project, where I used the DED Lua API to integrate an external program with the printer code. I interfaced with the printer through the HMI, where I created a simple button for the user that contains underlying Lua script code. This code links directly to the main lua script of the printer.

The external program contains three main subsections. The first is another Lua script, which is the link between my external program and the printer lua program. The second is a C# program, which reads in data from a laser distance sensor and sends the data to the lua script. The third is a C program, which I set up to directly communicate with the external lua script. I set up the C program for the next PhD student, who took over the next stage of the project.


**Measurement Equipment:**

I used a Keyence displacement laser IL-065 to measure the height of each layer in a print. To do this, I first manufactured a mount to attach the sensor to the print head. This is so that every time the print head moved up to create a new layer, the distance sensor moved the same amount. Thus, the goal of my control system was to make sure the distance remained constant every time the print head moved to the next layer. This constraint would then lead to constant layer heights, resulting in a more precise build height.


**Control System:**

I created a simple feedback controller that uses the data from the laser distance sensor to correct the error in height based on the readings of the print head z-axis.


**Results:**

Overall, I created an in-situ feedback control system for a LENS Multi-Metal DED Printer. The initial product of this project is a collaborative system between the printer and the user, where the user has to perform multiple steps to implement the control betwwen layers. This creates a bit of a timing inconsistency, which affects the overall results because it leads to different melt pool cooling rates between layers. The PhD student who took over the project after me is continuing my work to try to fully automate the system and implement more parameters into the control system.