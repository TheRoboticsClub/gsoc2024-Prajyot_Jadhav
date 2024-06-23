---
layout: post
title: "Week 4: June 17 ~ June 23"
date: 2024-06-22 18:01:00
description: New Gazebo Harmonic launcher for Robotics Application Manager
tags: 
categories: 
---

The goal for this week was to create a Gazebo Harmonic launcher for Robotics Application Manager (RAM) and to launch the Gazebo GUI from RAM. 

#### Objectives

- [x] Create a new Gazebo Harmonic launcher for Robotics Application Manager

#### Issues Fixed

- [https://github.com/JdeRobot/RoboticsApplicationManager/issues/135](https://github.com/JdeRobot/RoboticsApplicationManager/issues/135)

#### PRs Created

- [https://github.com/JdeRobot/RoboticsApplicationManager/pull/136](https://github.com/JdeRobot/RoboticsApplicationManager/pull/136)
- [https://github.com/JdeRobot/RoboticsInfrastructure/pull/400](https://github.com/JdeRobot/RoboticsInfrastructure/pull/400)

#### Work Done

- Created a config file for Gazebo GUI containing only the required plugins
- Migrated the Gazebo View launcher to Gazebo Harmonic by updating the commands used for configuring the browser screen dimensions for Gazebo GUI
- Resolved the black screen issue encountered for Gazebo GUI

Last week, I faced a black screen when launching the Gazebo GUI from another terminal inside the container while executing the first two steps of the dummy client. We discovered that the issue was due to models being added to the Gazebo world from [Gazebo Fuel](https://app.gazebosim.org/fuel) via SDF snippets (e.g., https://fuel.gazebosim.org/1.0/OpenRobotics/models/Coke). By removing the SDF snippets for the two models (sun and ground plane), the issue was resolved. I created an empty world file in RoboticsInfrastructure without the sun and ground plane models, which is used during dummy client testing.

<div class="row mt-3 justify-content-center">
    <div class="col-lg-10 mt-3 mt-md-0">
        {% include video.liquid path='assets/video/week4vdo1.mp4' class='img-fluid rounded z-depth-1' controls='true' %}
    </div>
</div>

I created a new config file containing only the required plugins, removing unnecessary elements from the Gazebo GUI. The essential plugins are MinimalScene and GzSceneManager, responsible for displaying the 3D scene. Additionally, I included InteractiveViewControl to allow user interaction with the GUI, such as moving the camera and zooming. I verified that the GUI dimensions could be adjusted by altering the width and height parameters in the config file.

{% include figure.liquid loading="eager" path="assets/img//week4/1.png" class="img-fluid rounded z-depth-1" zoomable=true %}

I updated the RAM launcher created in Week 2 of the coding period. The commands for configuring the browser screen dimensions for Gazebo GUI were updated. I successfully tested this launcher with the dummy client and was able to get a Gazebo Sim GUI on the web server.

<div class="row mt-3 justify-content-center">
    <div class="col-lg-10 mt-3 mt-md-0">
        {% include video.liquid path='assets/video/week4vdo2.mp4' class='img-fluid rounded z-depth-1' controls='true' %}
    </div>
</div>