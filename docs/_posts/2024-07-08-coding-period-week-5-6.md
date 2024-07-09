---
layout: post
title: "Week 5 and Week 6: June 24 ~ July 07"
date: 2024-07-08 21:01:00
description: New DDBB entry and migration of worlds and related files to Gz Harmonic
tags: 
categories: 
--- 

#### Objectives

- [x] Create a new Gazebo Harmonic launcher for Robotics Application Manager

#### Issues Fixed

- [https://github.com/JdeRobot/RoboticsAcademy/issues/2569](https://github.com/JdeRobot/RoboticsAcademy/issues/2569)
- [https://github.com/JdeRobot/RoboticsInfrastructure/issues/409](https://github.com/JdeRobot/RoboticsInfrastructure/issues/409)
- [https://github.com/JdeRobot/RoboticsInfrastructure/issues/406](https://github.com/JdeRobot/RoboticsInfrastructure/issues/406)
- [https://github.com/JdeRobot/RoboticsInfrastructure/issues/403](https://github.com/JdeRobot/RoboticsInfrastructure/issues/403)
- [https://github.com/JdeRobot/RoboticsAcademy/issues/2634](https://github.com/JdeRobot/RoboticsAcademy/issues/2634)
- [https://github.com/JdeRobot/RoboticsInfrastructure/issues/415](https://github.com/JdeRobot/RoboticsInfrastructure/issues/415)

#### PRs Created

- [https://github.com/JdeRobot/RoboticsAcademy/pull/2602](https://github.com/JdeRobot/RoboticsAcademy/pull/2602)
- [https://github.com/JdeRobot/RoboticsInfrastructure/pull/410](https://github.com/JdeRobot/RoboticsInfrastructure/pull/410)
- [https://github.com/JdeRobot/RoboticsInfrastructure/pull/413](https://github.com/JdeRobot/RoboticsInfrastructure/pull/413)
- [https://github.com/JdeRobot/RoboticsInfrastructure/pull/412](https://github.com/JdeRobot/RoboticsInfrastructure/pull/412)
- [https://github.com/JdeRobot/RoboticsAcademy/pull/2635](https://github.com/JdeRobot/RoboticsAcademy/pull/2635)
- [https://github.com/JdeRobot/RoboticsInfrastructure/pull/419](https://github.com/JdeRobot/RoboticsInfrastructure/pull/419)

#### Work Done

- Created a config file for Gazebo GUI containing only the required plugins
- Migrated the Gazebo View launcher to Gazebo Harmonic by updating the commands used for configuring the browser screen dimensions for Gazebo GUI
- Resolved the black screen issue encountered for Gazebo GUI

The issue ([#1152](https://github.com/gazebo-tooling/release-tools/issues/1152)), gazebo11-gz-cli PPA does not support ROS packages on Jammy, was resolved. So I was able to install Gazebo11 along with Gz Harmonic for the RADI. The issue encountered during the installation of the package `ros-humble-gazebo-ros` was resolved. The sourcing and compiling of the workspaces had previously been temporarily commented out. As the issues regarding the installation of dependencies was resolved, I was able to successfully build the workspaces.

I updated the hooks for the `CustomRobots` package and also updated the `.env` script for Gz Harmonic. During this migration I found that there is no separate model path for Gz sim, as it considers both models and worlds as resources. For Gazebo Classic the environment variables were `GAZEBO_MODEL_PATH` for models and `GAZEBO_RESOURCE_PATH` for worlds and some rendering resources, whereas that for Gz Sim is `GZ_SIM_RESOURCE_PATH` for worlds, models and other resources.

The world file for the rescue people exercise was migrated to Gz Harmonic using the previously migrated drone_assets. 

{% include figure.liquid loading="eager" path="assets/img//week3/2.png" class="img-fluid rounded z-depth-1" zoomable=true %}

<div class="caption">
    Rescue People world migrated to Gazebo Harmonic
</div>

The world for the follow road exercise was also migrated to Gazebo Harmonic. During this migration, I found that in the Gazebo Classic world file the road was included with a <road> tag, but it is not supported with Gz Sim <a href="https://github.com/gazebosim/gz-sim/issues/2320">(#2320)</a>. So for creating a road track, I created two models, one for a road curve and the other for a straight road. 

{% include figure.liquid loading="eager" path="assets/img//week3/2.png" class="img-fluid rounded z-depth-1" zoomable=true %}

<div class="caption">
    Follow Road world migrated to Gazebo Harmonic
</div>


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