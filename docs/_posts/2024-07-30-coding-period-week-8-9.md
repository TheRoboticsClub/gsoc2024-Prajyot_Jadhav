---
layout: post
title: "Week 8 and Week 9: July 15 ~ July 28"
date: 2024-07-08 21:01:00
description: Adding documentation and resolving errors for the new exercise
tags: 
categories: 
--- 

#### Objectives

- [x] Installation of Gazebo11 along with Gazebo Harmonic for the RADI
- [x] Updating CustomRobots Hooks and .env script for Gazebo Harmonic
- [x] Migration of Rescue people world and Follow Road world to Gazebo Harmonic
- [x] Creating a new DDBB entry for the Rescue People Harmonic exercise

#### Issues Fixed/Created

- [https://github.com/JdeRobot/RoboticsInfrastructure/issues/425](https://github.com/JdeRobot/RoboticsInfrastructure/issues/425)
- [https://github.com/JdeRobot/RoboticsApplicationManager/issues/143](https://github.com/JdeRobot/RoboticsApplicationManager/issues/143)
- [https://github.com/JdeRobot/RoboticsApplicationManager/issues/142](https://github.com/JdeRobot/RoboticsApplicationManager/issues/142)

#### PRs Created

- [https://github.com/JdeRobot/RoboticsApplicationManager/issues/143](https://github.com/JdeRobot/RoboticsApplicationManager/issues/143)
- [https://github.com/JdeRobot/RoboticsApplicationManager/pull/148](https://github.com/JdeRobot/RoboticsApplicationManager/pull/148)

#### Work Done

The issue with the gazebo11-gz-cli PPA not supporting ROS packages on Jammy ([#1152](https://github.com/gazebo-tooling/release-tools/issues/1152)) has been resolved. This allowed me to successfully install Gazebo11 along with Gz Harmonic for the RADI. Previously, I encountered an issue during the installation of the `ros-humble-gazebo-ros` package, but that has now been fixed. Initially, I had temporarily commented out the sourcing and compiling of the workspaces. However, with the dependency installation issues resolved, I was able to build the workspaces successfully.

I updated the hooks for the `CustomRobots` package and the `.env` script for Gz Harmonic. During this migration, I discovered that Gz Sim does not have a separate model path, as it treats both models and worlds as resources. In Gazebo Classic, the environment variables `GAZEBO_MODEL_PATH` were used for models and `GAZEBO_RESOURCE_PATH` for worlds and some rendering resources. However, in Gz Sim, `GZ_SIM_RESOURCE_PATH` is used for worlds, models, and other resources.

The world file for the rescue people exercise was migrated to Gz Harmonic using the previously migrated drone_assets.

{% include figure.liquid loading="eager" path="assets/img//week56/1.png" class="img-fluid rounded z-depth-1" zoomable=true %}

<div class="caption">
    Rescue People world migrated to Gazebo Harmonic
</div>

Similarly, the world for the follow road exercise was also migrated to Gazebo Harmonic. During this process, I found that the `<road>` tag used in the Gazebo Classic world file is not supported in Gz Sim [(#2320)](https://github.com/gazebosim/gz-sim/issues/2320). To address this, I created two new models for the road track: one for curves and another for straight sections.

{% include figure.liquid loading="eager" path="assets/img//week56/2.png" class="img-fluid rounded z-depth-1" zoomable=true %}

<div class="caption">
    Follow Road world migrated to Gazebo Harmonic
</div>

A database entry was created for the Rescue People Gz Harmonic exercise. Also, a new Gz Sim world type for the exercise template was created by migrating the Django model. With this new world type, the Gz Sim launcher from RAM will be used to launch the Gazebo GUI.

{% include figure.liquid loading="eager" path="assets/img//week56/3.png" class="img-fluid rounded z-depth-1" zoomable=true %}