---
layout: post
title: "Week 10: July 29 ~ August 04"
date: 2024-08-05 21:01:00
description:  Fixing issues with the functionality of the Play, Pause, and Reset buttons for the Gz Harmonic exercise
tags: 
categories: 
--- 

#### Objectives

- [x] Resolving functionality issues with the Play and Pause buttons
- [ ] Addressing and fixing problems related to the Reset button's operation (solved partially)

#### Work Done

In the previous week, I encountered issues where images on the GUI server were not updating as expected. Additionally, the Play button failed to toggle to Pause when the application was running, and the Reset button remained grayed out.

Upon investigation, I identified the potential cause within the Robotics Application Manager, specifically within the `run_application`, `pause`, `resume`, and `terminate` transitions. In the `run_application` transition, the `unpause_sim` function was being called, while the `pause_sim` and `reset_sim` functions were invoked in the `terminate` transition.

For the Gazebo Classic simulator integrated with ROS 2, pausing, unpausing, and resetting simulations are managed through ROS 2 services. The following commands are used in the command line:

- To ( un )pause:
  ```
  ros2 service call /(un)pause_physics std_srvs/srv/Empty
  ```

- To reset:
  ```
  ros2 service call /reset_world std_srvs/srv/Empty
  ```

However, in the newer Gazebo Sim, the approach has shifted from ROS 2 services to Gazebo (gz) services for these operations. 

A Gazebo transport API is now available for starting, stopping, and resetting the simulation. This is done via the command line by calling the service `/world/<world_name>/control` and filling the request with the message type `gz.msgs.WorldControl`. This service responds with a `gz.msgs.Boolean` indicating the success (`true`) or failure (`false`) of the request.

To control the simulation:

- **Start the simulation:**
  ```
  gz service -s /world/<world_name>/control --reqtype gz.msgs.WorldControl --reptype gz.msgs.Boolean --timeout 3000 --req 'pause: false'
  ```

- **Pause the simulation:**
  ```
  gz service -s /world/<world_name>/control --reqtype gz.msgs.WorldControl --reptype gz.msgs.Boolean --timeout 3000 --req 'pause: true'
  ```

- **Reset the simulation:**
  ```
  gz service -s /world/<world_name>/control --reqtype gz.msgs.WorldControl --reptype gz.msgs.Boolean --timeout 3000 --req 'reset: {all: true}'
  ```

The reset operation, similar to the pause and unpause commands, is managed through the same service. The `reset` field in the `gz.msgs.WorldControl` message allows you to reset the world to time zero. When executed, this command stops the simulation and resets the world state, with the success of the request indicated by the returned Boolean value.

Since the Gazebo (gz) services include the `<world_name>` in their paths, I implemented a solution to ensure compatibility across different exercises with varying world names. I used a regular expression `$(gz service -l | grep '^/world/\w*/control$')` to dynamically identify the correct service name from the available services. This approach works well, as only one exercise is run at a time, each with its specific world name.

I then updated the `unpause_sim` and `pause_sim` functions in the RoboticsApplicationManager for `visualization_type` as `gzsim_rae`. With these updates, I successfully resolved the issues related to the Play/Pause functionality and the problem with static images.

<div class="row mt-3 justify-content-center">
    <div class="col-lg-10 mt-3 mt-md-0">
        {% include video.liquid path='assets/video/week10vdo1.mp4' class='img-fluid rounded z-depth-1' controls='true' %}
    </div>
</div>

<div class="caption">
    Play/Pause Functionality Demonstration
</div>

However, when I applied similar updates to the `reset_sim` function, the simulation didn't perform as expected, and Gazebo Sim crashed. The service worked fine with basic simulation environments but specifically failed when using Aerostack2. After discussing this with the mentors, we hypothesized that the issue might be related to the Aerostack2 bridges not being reset correctly.

To work around this problem, I initially attempted to delete the quadrotor model and respawn it at its initial position, but this also caused the simulation to crash. Instead, I implemented a solution that involves resetting the pose of the quadrotor model to its initial position when the reset button is clicked. This approach works well since, in the Rescue People exercise, the quadrotor is the only dynamic model in the simulation environment.

The command to reset the drone's position is:

```
gz service -s /world/<world_name>/set_pose --reqtype gz.msgs.Pose --reptype gz.msgs.Boolean --timeout 300 --req 'name: "drone0", position: {x: 0, y: 0, z: 0}'
```

This successfully resets the drone to its initial position. However, I've encountered a new issue: when re-running the code after resetting, the drone doesn't perform a takeoff and instead directly moves to the setpoint position. I will investigate and try to resolve this next.

<div class="row mt-3 justify-content-center">
    <div class="col-lg-10 mt-3 mt-md-0">
        {% include video.liquid path='assets/video/week10vdo2.mp4' class='img-fluid rounded z-depth-1' controls='true' %}
    </div>
</div>

<div class="caption">
    Reset Functionality: Quadrotor Returning to Initial Position
</div>