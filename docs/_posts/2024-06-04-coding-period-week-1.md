---
layout: post
title: "Week 1: May 27 ~ June 02"
date: 2024-06-04 21:01:00
description: Creating and testing a new RADI with Gazebo Harmonic
tags: 
categories: 
---

The goal for this week was to modify the Dockerfiles to create a new RADI with Gazebo Harmonic and test it with xhost +.

#### Objectives

- [x] Create and test a new RADI with Gazebo Harmonic

#### Issues Fixed

- [https://github.com/JdeRobot/RoboticsAcademy/issues/2540](https://github.com/JdeRobot/RoboticsAcademy/issues/2540)

#### PRs Created

- [https://github.com/JdeRobot/RoboticsAcademy/pull/2542](https://github.com/JdeRobot/RoboticsAcademy/pull/2542)

#### Work Done

- Modified Dockerfiles to:
  - Replace Gazebo 11 with Gazebo Harmonic
  - Remove the installation of PX4 and MICRO-XRCE-DDS-AGENT
  - Remove the cloning of as2_platform_pixhawk and px4_msgs repositories
- Determined that the CustomRobots package has gazebo-ros and gazebo-ros2-control as dependencies
- Checked out the installation of Gazebo 11 along with Gazebo Harmonic

I encountered the following error while building an image from the modified Dockerfiles. Replacing Gazebo11 with Gazebo Harmonic caused installation failures for `gazebo-ros2-control` and `gazebo-ros` during `rosdep install`. These are the dependencies for the CustomRobots package, as specified in its [package.xml](https://github.com/JdeRobot/RoboticsInfrastructure/blob/humble-devel/CustomRobots/package.xml) file. To address this, the sourcing and compiling of the workspace have been temporarily commented out.

{% include figure.liquid loading="eager" path="assets/img//week1/1.png" class="img-fluid rounded z-depth-1" zoomable=true %}

Additionally, I tested whether Gazebo11 can be installed alongside Gazebo Harmonic by following the instructions in [Installing Gazebo11 side by side with new Gazebo](https://github.com/gazebosim/docs/blob/master/install_gz11_side_by_side.md). However, I found that these instructions resulted in only Gazebo Harmonic being installed.

#### RADI with Gazebo Harmonic

<div class="row mt-3 justify-content-center">
    <div class="col-lg-10 mt-3 mt-md-0">
        {% include video.liquid path='assets/video/week1.mp4' class='img-fluid rounded z-depth-1' controls='true' %}
    </div>
</div>

<!-- <div class="caption">
    New RADI with Gazebo Harmonic (with xhost +)
</div> -->