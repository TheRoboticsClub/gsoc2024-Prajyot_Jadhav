---
layout: post
title: "Week 2: June 03 ~ June 09"
date: 2024-06-10 15:01:00
description: Creating new Gazebo Harmonic launcher for Robotics Application Manager
tags: 
categories: 
---

This week I focused on creatiing a new Gazebo Harmonic launcher for Robotics Application Manager.

#### Objectives

- [ ] Create a new Gazebo Harmonic launcher for Robotics Application Manager

#### Work Done

- Understood the code of the existing Gazebo View launcher and the related files for Docker Threading and VNC server
- By referring to the old Gazebo View launcher, created a new launcher for Gazebo Harmonic by:
  - Updating the commands used for configuring the browser screen dimensions for Gazebo GUI
  - Replacing the commands for starting gzclient with those for starting Gazebo Sim's GUI
- Created a new RADI with installation of Gazebo 11 along with Gazebo Harmonic

In the old Gazebo View launcher, `gui.ini` file was modified to set the geometry of the Gazebo client window. The `gui.ini` file is a configuration file used by Gazebo Classic to store settings related to the graphical user interface. This file contains parameters that control the appearance of the Gazebo GUI, such as window size and position. 

The new Gazebo Sim does not use a `gui.ini` file for GUI configurations. Instead, GUI configurations are handled through XML configuration files that define what the window should look like and which plugins should be loaded. By default, Gazebo GUI will load the config file at `$HOME/.gz/gui/default.config`, if it exists.

For Gazebo Classic, the `gazebo` command runs two different executables, `gzserver` and second `gzclient`. The gzclient executable runs a QT based user interface that visualizes the simulation and provides control over various simulation properties.
For Gazebo sim the `gz sim` command launches both the Sim server and Sim GUI. The GUI can be run independently using the `-g` (gui only) flag.

{% include figure.liquid loading="eager" path="assets/img//week2/week2.png" class="img-fluid rounded z-depth-1" zoomable=true %}

Also, Pedro had raised a issue for the [Installing Gazebo11 side by side with new Gazebo not working](https://github.com/gazebosim/docs/issues/449), which was resolved. I created a new RADI with both Gazebo 11 and Gazebo Harmonic installed. However, I still encountered installation failures for `gazebo-ros2-control` and `gazebo-ros` during `rosdep install`. The sourcing and compiling of the workspace has been temporarily commented out until we can address this issues.

#### RADI with Gazebo 11 and Gazebo Harmonic

<div class="row mt-3 justify-content-center">
    <div class="col-lg-10 mt-3 mt-md-0">
        {% include video.liquid path='assets/video/week2vdo1.mp4' class='img-fluid rounded z-depth-1' controls='true' %}
    </div>
</div>

<!-- <div class="caption">
    New RADI with Gazebo Harmonic (with xhost +)
</div> -->