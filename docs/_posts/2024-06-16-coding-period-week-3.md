---
layout: post
title: "Week 3: June 10 ~ June 16"
date: 2024-06-17 21:01:00
description: Migration of drone_assets to Gazebo Harmonic 
tags: 
categories: 
---

The goal for this week was to migrate the models in [drone_assets](https://github.com/JdeRobot/RoboticsInfrastructure/tree/humble-devel/CustomRobots/drone_assets) to Gazebo Harmonic.

#### Objectives

- [x] drone_assets migration to Gz Harmonic

#### Issues Fixed

- [https://github.com/JdeRobot/RoboticsInfrastructure/issues/401](https://github.com/JdeRobot/RoboticsInfrastructure/issues/401)

#### PRs Created

- [https://github.com/JdeRobot/RoboticsInfrastructure/pull/402](https://github.com/JdeRobot/RoboticsInfrastructure/pull/402)

#### Work Done

- Updated the simple_circuit_followingcam.launch.py file for dummy client testing
- Determined the issue with commands used for configuring the browser screen dimensions for Gazebo GUI
- Migrated drone_assets to Gazebo Harmonic

Last week, I encountered difficulties while testing the new RAM launcher with the dummy client.  During our meeting, Pedro guided me on debugging and development with the dummy client. In the dummy client, for the second step of `launch_world`, the `simple_circuit_followingcam.launch.py` file is launched. My focus was on modifying this file to make it compatible with Gazebo Harmonic. I updated the file, replacing `gazebo_ros` with `ros_gz` and the `gzserver.launch.py` file with the corresponding one from the `ros_gz` package. Using the dummy client, I successfully executed the first two steps: `connect` and `launch_world`. The third step, `prepare_visualization`, which launches the Gazebo GUI, was commented out. I managed to launch the Gazebo GUI from another terminal inside the container, but encountered a black screen. Running the `gz sim -g` command with the `-v4` argument showed that the GUI was requesting a list of world names and the server was downloading resources. I am currently working on resolving this issue.

<div class="row mt-3 justify-content-center">
    <div class="col-lg-10 mt-3 mt-md-0">
        {% include video.liquid path='assets/video/week3vdo1.mp4' class='img-fluid rounded z-depth-1' controls='true' %}
    </div>
</div>

<!-- <div class="caption">
    New RADI with Gazebo Harmonic (with xhost +)
</div> -->

Previously, I had found that the default configuration file for the Gazebo SIM GUI is located at `$HOME/.gz/gui/default.config`. However, for Gazebo Harmonic, the correct path is `$HOME/.gz/sim/<#>/gui.config` (where <#> represents Gazebo Sim's major version). I attempted to launch an empty_world with a modified config file specifying only the window dimensions. However, I observed that a specific set of plugins is necessary to launch an empty_world, and if these are missing, the default config file is used. My next task would be to create a new config file containing only the required plugins, removing unnecessary elements from the Gazebo GUI.

While migrating models in drone_assets to Gazebo Harmonic, I discovered that Gazebo SIM does not support Ogre material files like Classic does, due to its compatibility with multiple rendering engines. In Gazebo Sim, textures can be passed as the albedo map. Therefore, in the sdf files of the models the following code:

```
<material>
  <script>
    <uri>model://number1/materials/scripts</uri>
    <uri>model://number1/materials/textures</uri>
    <name>Number/One</name>
  </script>
</material>
```
was replaced with:
```
<material>
  <pbr>
    <metal>
      <albedo_map>model://number1/materials/textures/texture.png</albedo_map>
    </metal>
  </pbr>
</material>
```
I added new models for ocean and polaris_ranger_ev. The models yet to be migrated are: gas_station, house_3, UAVs (iris and typhoon h480). Also the system plugin `libwall2plugin.so` used in the cylinder and wall models is to be migrated.

{% include figure.liquid loading="eager" path="assets/img//week3/2.png" class="img-fluid rounded z-depth-1" zoomable=true %}

<div class="caption">
    Models from Rescue People exercise migrated to Gazebo Harmonic
</div>