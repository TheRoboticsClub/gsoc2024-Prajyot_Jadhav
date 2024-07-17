---
layout: post
title: "Week 7: July 08 ~ July 14"
date: 2024-07-16 12:01:00
description: Updating Aerostack2 launcher for Gz Sim
tags: 
categories: 
--- 

#### Objectives

- [x] Updating the DDBB entry for Rescue People Harmonic exercise
- [x] Updating drones_ros2 launcher to launch the Aerostack2 Gz Sim launcher
- [x] Updating the Aerostack2 launcher for Gz Sim

#### Issues Fixed

- [https://github.com/JdeRobot/RoboticsInfrastructure/issues/422](https://github.com/JdeRobot/RoboticsInfrastructure/issues/422)

#### PRs Created

- [https://github.com/JdeRobot/RoboticsApplicationManager/pull/138](https://github.com/JdeRobot/RoboticsApplicationManager/pull/138)
- [https://github.com/JdeRobot/RoboticsInfrastructure/pull/423](https://github.com/JdeRobot/RoboticsInfrastructure/pull/423)

#### Work Done

Last week, I created a new `Gz Sim` world type for the exercise template by migrating the Django model. However, while reviewing the RoboticsApplicationManager codebase, I discovered that the GazeboView launcher is launched during the visualization step. Consequently, I had to revert the previous week's changes and create two new visualization options: `Gz Sim GRA` and `Gz Sim RAE`. Now, when these fields are selected for visualization, the new Gz Sim launcher is launched for the Gazebo Sim GUI.

Next, I updated the drones_ros2 launcher, which is used for the drones and ROS2 world type. Instead of launching the `aerostack2_default_gazebo_classic` launch file, it now launches the `aerostack2_default_gazebo_sim` launch file from the `jderobot_drones` package.

I updated the `aerostack2_default_gazebo_sim` launch file to launch the `as2_platform_gazebo` and `as2_gazebo_assets` packages. The `as2_gazebo_assets` package is now launched in headless mode. This means that only the Gazebo server is started, without the GUI. The Gazebo GUI can be launched separately during the visualization step using the new Gz Sim launcher.

{% include figure.liquid loading="eager" path="assets/img//week7/1.png" class="img-fluid rounded z-depth-1" zoomable=true %}

<div class="caption">
    Rescue People exercise
</div>

However, I am currently facing two issues. The world starts at the default camera position rather than the one specified in the SDF file of the world. Also, I am encountering an error with the HAL functions: `Service drone0                                                             /controller/set_control_mode is not available`

{% include figure.liquid loading="eager" path="assets/img//week7/2.png" class="img-fluid rounded z-depth-1" zoomable=true %}
