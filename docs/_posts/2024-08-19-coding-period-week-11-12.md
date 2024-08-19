---
layout: post
title: "Week 11 and Week 12: August 05 ~ August 18"
date: 2024-08-18 01:01:00
description:  Creating a new RAM world type and fixing issues with Reset functionality for the Gz Harmonic exercise
tags: 
pretty_table: true
categories: 
--- 

#### Objectives

- [x] Creating a new RAM world type for Gz Sim Drone based exercises
- [ ] Addressing and fixing problems related to the Reset button's operation

#### Work Done

In our previous meeting, the mentors recommended making changes to the existing Pull Requests by creating a separate launcher for drones for the `as2_gazebo_sim` file. Following this advice, I created a new world type, `Gz Sim Drones`, by migrating the Django model. This new world type launches a new `drones_gzsim` launcher, which in turn starts the Aerostack2 Gazebo Sim launch file. This approach ensures that the previous drone-based exercises remain unaffected, providing a fallback option in case any issues arise with the newly migrated exercise.

{% include figure.liquid loading="eager" path="assets/img//week12/frames.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}

Previously, for the Rescue People exercise, the drone's position was reset to its initial location using hardcoded values. Pedro suggested an improved solution to make this approach adaptable for different drone-based exercises. As shown in the transform tree figure, there is a static `drone0/map` frame located at the initial spawn point of the quadrotor. By determining the transform between the `earth` frame (located at coordinates (0,0,0)) and the `drone0/map` frame, we can accurately calculate the quadrotor's initial position. This position will then be used in the Gazebo service to set the quadrotor model's pose.

Regarding the issue where the quadrotor fails to take off after resetting, Pedro suggested that this might be due to the Aerostack2 state machine not updating post-reset.

The Aerostack2 states and transitions are as follows:

**States:**
- TAKING_OFF
- FLY
- LANDING
- LANDED
- DISARMED
- EMERGENCY

**Transitions:**

| **Current State** | **Event** | **Next State** |
| :----------- | :------------ | :------------ |
| TAKING_OFF       |    TOOK_OFF    |       FLY |
| FLY       |    LAND    |       LANDING |
| LANDING       |    LANDED    |       LANDED |
| LANDED       |    TAKE_OFF    |       TAKING_OFF |
| LANDED       |    DISARM    |       DISARMED |
| DISARMED       |    ARM    |       LANDED |
| FLY, LANDING, LANDED, TAKING_OFF       |    EMERGENCY    |       EMERGENCY |


When the drone's position is reset to its initial location, it remains in the `FLY` state, preventing it from performing a takeoff. Therefore, the Aerostack2 state must also be updated to `LANDING` and then to `LANDED` during the reset process.

To address this, I attempted to create a ROS2 service to reset the quadrotor's pose and update the Aerostack2 state machine. Initially, I implemented the service within the `drone_wrapper` file but encountered an issue where the application would pause when the reset button was clicked, rendering the service unavailable. This occurs because the `terminate_application` function is triggered upon pressing the reset button, where the application first pauses before resetting.

To resolve this, I created a new `DroneWrapper` object within the reset function before calling the service. However, this resulted in a black screen appearing on the VNC server instead of the expected Gazebo Sim simulation.

To work around this, I created a new file, `drone_reset.py`, with a `quadrotor_reset` node specifically for the service. I then created a `DroneReset` class object in the reset function and called the ROS2 service. 

{% include figure.liquid loading="eager" path="assets/img//week12/1.png" class="img-fluid rounded z-depth-1" zoomable=true %}

<div class="caption">
    \quadrotor_reset_pose ROS2 service
</div>

Although the service is now available, it’s currently getting stuck at `requester: making request: std_srvs.srv.Trigger_Request()`.

{% include figure.liquid loading="eager" path="assets/img//week12/2.png" class="img-fluid rounded z-depth-1" zoomable=true %}