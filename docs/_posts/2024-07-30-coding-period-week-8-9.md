---
layout: post
title: "Week 8 and Week 9: July 15 ~ July 28"
date: 2024-07-29 21:01:00
description: Adding documentation and fixing errors for the Rescue People Gz Harmonic exercise
tags: 
categories: 
--- 

#### Objectives

- [x] Adding documentation for creating a new RAM launcher and a guide for using the dummy RAM client
- [x] Resolving issues with HAL functions in the Rescue People Gz Harmonic exercise
- [x] Troubleshooting and resolving problems with image display on the GUI
- [ ] Fixing issues with the functionality of the Play, Pause, and Reset buttons

#### Issues Fixed

- [https://github.com/JdeRobot/RoboticsApplicationManager/issues/143](https://github.com/JdeRobot/RoboticsApplicationManager/issues/143)
- [https://github.com/JdeRobot/RoboticsApplicationManager/issues/142](https://github.com/JdeRobot/RoboticsApplicationManager/issues/142)

#### PRs Created

- [https://github.com/JdeRobot/RoboticsApplicationManager/issues/143](https://github.com/JdeRobot/RoboticsApplicationManager/issues/143)
- [https://github.com/JdeRobot/RoboticsApplicationManager/pull/148](https://github.com/JdeRobot/RoboticsApplicationManager/pull/148)

#### Work Done

I have added a guide to the RoboticsApplicationManager repository for using the dummy RAM client, which aids in developing and debugging new RAM launchers. Also, I documented the steps for creating a new RAM launcher, detailing the necessary changes and new files to be created for the `launch_world` and `prepare_visualization` transitions. This documentation is intended to assist new contributors in the development of RAM launchers.

Last week, I encountered an issue with the HAL functions for the Rescue People Harmonic exercise. The problem arose because I renamed the folder containing the config files for the `as2_state_estimator` and `as2_motion_controller` packages from `ign` to `gzsim` but did not update the path in the `setup.py` file. Consequently, the config files were not found in the share directory during launch, causing the launch file to fail. Modifying the `setup.py` file of the `jderobot_drones` package resolved the issue.

<div class="row mt-3 justify-content-center">
    <div class="col-lg-10 mt-3 mt-md-0">
        {% include video.liquid path='assets/video/week8vdo1.mp4' class='img-fluid rounded z-depth-1' controls='true' %}
    </div>
</div>

However, I was still facing some issues. As it can be seen in the video above, I could use functions from HAL, but I was unable to display images using `GUI.showImage(cv2_image)` and `GUI.showLeftImage(cv2_image)`. Additionally, when running the code, the play button did not change to pause, and the reset button remained grayed out.

To resolve this, I first checked if data was being received on the two topics for images: `drone0/sensor_measurements/frontal_camera/image_raw` and `drone0/sensor_measurements/ventral_camera/image_raw`. I observed that no data was being published on `drone0/sensor_measurements/frontal_camera/image_raw`, but data was present on `drone0/sensor_measurements/front_camera/image_raw`. After discussing with mentors, I learned that the image topic for the front camera depends on how the camera is included in the simulation config file used for the `as2_gazebo_assets` package. If the payload's "model_name" is set to "frontal_camera," data is obtained on `/frontal_camera/image_raw`; if it is "front_camera," data is obtained on `/front_camera/image_raw`. I adjusted the `sim_config` file for the Rescue People Gz Harmonic Exercise accordingly. Also, I updated some outdated paths in the HTML file of the new exercise.
Despite these changes, the image display issue remained unresolved. The mentors recommended examining the RoboticsApplicationManager code for potential issues.

I discovered that in the Robotics Application Manager, during the `prepare_visualization` transition from the `world_ready` to the `visualization_ready` state, a GUI server was started only if the `visualization_type` was `gazebo_rae`. I modified this configuration so that the GUI server also starts when the `visualization_type` is `gzsim_rae`. Following these changes, the images were displayed on the GUI; however, they were not updating and remained fixed at the initial image.

In addition to the issue of static images, the play/pause and reset buttons are still not functioning as expected.

{% include figure.liquid loading="eager" path="assets/img//week8/1.png" class="img-fluid rounded z-depth-1" zoomable=true %}