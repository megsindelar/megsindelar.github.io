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
The goal of this project was to design and implement a signature-based feedback control system on a Multi-Metal DED Printer.
"Image"
  

This was my project as a Research Assistant at the University of Wisconsin-Madison. There were three overall stages, the first of which I was tasked with. My stage was to create a feedback control system for the build height of a print, both in-situ and ex-situ, as an initial proof of concept. I was the sole individual on this part of the project.

This first project staged contained three main parts, including software integration, measurement equipment, and the control system. 

Software Integration:
    This was the biggest part of my project, where I used the DED Lua API to integrate an external program with the printer code. I interfaced with the printer through the HMI, where I created a simple button for the user that contains underlying Lua script code. This code links directly to the main lua script of the printer.

    The external program contains three main subsections. The first is another Lua script, which is the link between my external program and the printer lua program. The second is a C# program, which reads in data from a laser distance sensor and sends the data to the lua script. The third is a C program, which I set up to directly communicate with the external lua script. I set up the C program for the next PhD student, who took over the next stage of the project.


Measurement Equipment:
    


Control System:
    I created a simple feedback controller that uses the data from the laser distance sensor and corrects the height error based on the reading of the print head z-axis.

