---
layout: post
read_time: false
show_date: false
title: "Sindelar - Feedback Control on a Multi-Metal DED Printer"
# date: 2021-01-06 #2021-01 - 2021-06
img: posts/Feedback_Height/Feedback_Height_Cover.jpg
# tags: [C, Lua, C#, Controls, 3D-printing]
#category: 
author: Meg Sindelar
description: 
---
The goal of this project was to design and implement a signature-based feedback control system on a LENS Multi-Metal DED Printer.

Software: Lua Script, C#, C

Hardware: LENS MR 7 printer, Keyence IL-065 laser, NI USB-6000 A/D converter


This was my project as a Research Assistant at the University of Wisconsin-Madison. There were three overall stages, the first of which I was tasked with. My stage was to create a feedback control system for the build height of a print, both in-situ and ex-situ, as an initial proof of concept. I was the sole individual on this part of the project. The system layout for the project is shown below.

![Screenshot from 2022-11-10 20-16-17](https://user-images.githubusercontent.com/87098227/201492181-68731637-6cfc-47ae-80ea-8ae004756e3b.png)

My stage of the project staged contained three main parts, including software integration, measurement equipment, and the control system. 

**Software Integration:**

This was the main part of my project, where I used the LENS Lua API to integrate an external program with the printer code. I interfaced with the printer through the HMI, where I created a simple button for the user that contains underlying Lua script code. This code links directly to the main lua script of the printer.

The external program contains three main subsections. The first is another Lua script, which is the link between my external program and the printer lua program. The second is a C# program, which reads in data from a laser distance sensor and sends it to the external Lua script. The third is a C program, which I set up to directly communicate with the external lua script. I set this C program up for the PhD student who took over the next stage of the project.


**Measurement Equipment:**

I used a Keyence IL-065 displacement laser to measure the height of each layer in a print. To do this, I first manufactured a mount to attach the sensor to the print head. This is so that every time the print head moved up to create a new layer, the distance sensor moved the same amount. Thus, the goal of my control system was to make sure the distance remained constant each time the print head moved to the next layer. This constraint would then lead to constant layer heights, resulting in a more precise build height. I used a C# program to process the data, as specified by the documentation. An image of the laser measuring a print build is shown below by the red dot on the part.

![Feedback_Height_Laser](https://user-images.githubusercontent.com/87098227/208274457-98eb5cc6-75e9-44a7-8f69-183eff8702aa.jpg)

I also used a NI USB-6000 A/D converter to convert the analog data from the laser distance sensor to digital for the C# program.


**Control System:**

I created a simple feedback controller that uses the data from the laser distance sensor to correct for the error in height, based on the readings of the print head z-axis. I also set up a model for a PID controller for the next student, which will be implemented when the student tries to control more print parameters.


**Results:**

Overall, I created an in-situ feedback control system for a LENS Multi-Metal DED Printer. The initial product of this project is a collaborative system between the printer and the user, where the user has to perform multiple steps to implement the control betwwen layers. This creates a bit of a timing inconsistency, which affects the overall results because it leads to different melt pool cooling rates between layers. The PhD student who took over the project after me is continuing my work to try to fully automate the system and implement more parameters into the control system.
