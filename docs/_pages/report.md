---
layout: report
permalink: /report/
title: report
heading: "Final Report"
date: 2024-08-21 00:01:00
pretty_table: true
categories: 
nav: true
nav_order: 5
toc: true
toc:
  beginning: true
images:
  compare: true
  slider: true
--- 

## Robotics-Academy: Migration to Gazebo Harmonic

<hr>

<!-- > **Organization**: [JdeRobot](https://jderobot.github.io/)  
> **Mentors**: Pedro Arias-Perez, Pawan Wadhwani, Miguel Fernandez-Cortizas, Apoorv Garg  
> **Student**: Prajyot Jadhav ([GitHub](https://github.com/Arcane-01), [LinkedIn](https://www.linkedin.com/in/prajyot-jadhav-90921a241/))  
> **Link to GSoC Project**: [Robotics-Academy: Migration to Gazebo Harmonic](https://summerofcode.withgoogle.com/programs/2024/projects/CgRdpsST) -->

**Organization**: [JdeRobot](https://jderobot.github.io/)  
**Mentors**: Pedro Arias Pérez, Pawan Wadhwani, Miguel Fernández Cortizas, Apoorv Garg
**Student**: Prajyot Jadhav ([GitHub](https://github.com/Arcane-01), [LinkedIn](https://www.linkedin.com/in/prajyot-jadhav-90921a241/))  
**Link to GSoC Project Page**: [Robotics-Academy: Migration to Gazebo Harmonic](https://summerofcode.withgoogle.com/programs/2024/projects/CgRdpsST)

Hello everyone,

This summer, I had the opportunity to contribute to Robotics-Academy through the Google Summer of Code 2024 program. My project focused on upgrading the Robotics-Academy's Docker-based framework by migrating it to Gazebo Harmonic from Gazebo Classic, ensuring the platform's long-term compatibility. My project proposal can be found [here](https://theroboticsclub.github.io/gsoc2024-Prajyot_Jadhav/assets/pdf/JdeRobot_proposal.pdf).

### About me

I have a Bachelor's degree in Electronics and Communication Engineering from Visvesvaraya National Institute of Technology, India. My interests lie in robotics and control systems. Google Summer of Code 2024 marked my first substantial contribution to open source, and it was an amazing experience.

### About the Project

JdeRobot's Robotics-Academy provides exercises to learn robotics and AI while abstracting students from the complexities of the framework. The dockerized containers and web templates offer cross-platform functionality, simplifying the setup process. This allows beginners to focus on coding and testing their algorithms without dealing with extensive software installation.

Currently, Robotics-Academy uses Gazebo11 in the Robotics-Academy Docker Image (RADI) framework. The primary goal of my project was to migrate the RADI to Gazebo Harmonic and update exercises accordingly. Also, I replaced PX4 with the lighter Aerostack2 Gazebo platform for drone-based exercises, enhancing efficiency.

### Contribution Summary
<hr>

#### Stage 1: Modifying Models and World SDF Files

<swiper-container keyboard="true" navigation="true" pagination="true" pagination-clickable="true" pagination-dynamic-bullets="true" rewind="true">
   <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/week56/2.png" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/week56/1.png" class="img-fluid rounded z-depth-1" %}</swiper-slide>
</swiper-container>

This stage involved updating the drone-based exercise models and creating new SDF files for the worlds to ensure compatibility with the latest version of Gazebo. For models that were challenging to migrate and for which new open-source alternatives were available, I incorporated these new models. Adjustments were made to plugins, parameters, and configurations in the SDF files to align with the updated Gazebo setup.

#### Stage 2: Installing Dependencies and Updating Files  

In this stage, I installed Gazebo Harmonic within the Docker image to support the migration process. Given that most Robotics-Academy exercises are currently in Gazebo 11, I ensured compatibility by installing both Gazebo Harmonic and Gazebo 11. This approach allows exercises still using Gazebo 11 to remain operational. Additionally, I updated hooks for certain packages and modified files, such as the Robotics Application Manager file, to support the new Gazebo Sim exercises.

#### Stage 4: Modifying the Database and Adding New Fields for Gazebo Sim Exercises

In Robotics-Academy, each exercise is represented as a database entry, including fields such as "visualisation" and "world". These fields determine the launch files used by the Robotics Application Manager. I updated the Django model to include new options for "visualisation" and "world" specific to Gazebo Sim exercises. A new entry was also created for the Rescue People exercise, which was migrated to Gazebo Harmonic.

#### Stage 4: Creating New Launchers for Gazebo Sim Exercises  

For the newly added "visualisation" and "world" fields related to Gazebo Sim exercises, I developed new launchers within the Robotics Application Manager. These launchers facilitate the launch of the Gazebo Sim GUI server and the Aerostack2 launch file. The Aerostack2 launcher was updated to support Gazebo Sim and to replace PX4 with the Aerostack2 Gazebo Platform.

#### On GitHub

Over the summer, I submitted 14 pull requests, all of which have been merged. These pull requests addressed 12 issues, and my contributions will be incorporated into the upcoming releases of JdeRobot's Robotics-Academy.

<table>
    <thead>
        <tr>
            <th>Pull Request</th>
            <th>Solves Issue</th>
            <th>Description</th>
            <th>More</th>
        </tr>
    </thead>
    <tbody>
        <tr>
             <td colspan="4"><a href="https://github.com/JdeRobot/RoboticsAcademy">Robotics-Academy</a></td>
        </tr> 
        <tr>
            <td><a href="https://github.com/JdeRobot/RoboticsAcademy/pull/2542">#2542</a></td>
            <td><a href="https://github.com/JdeRobot/RoboticsAcademy/issues/2540">#2540</a></td>
            <td>New Robotics-Academy Docker Image including Gazebo Harmonic</td>
            <td><a href="https://theroboticsclub.github.io/gsoc2024-Prajyot_Jadhav/blog/2024/coding-period-week-1/">Week-1 Blog</a></td>
        </tr>
        <tr>
            <td><a href="https://github.com/JdeRobot/RoboticsAcademy/pull/2602">#2602</a></td>
            <td><a href="https://github.com/JdeRobot/RoboticsAcademy/issues/2569">#2569</a></td>
            <td>Updated Dockerfiles for Gazebo11 installation along with Gazebo Harmonic</td>
            <td><a href="https://theroboticsclub.github.io/gsoc2024-Prajyot_Jadhav/blog/2024/coding-period-week-5-6/">Week-5, 6 Blog</a></td>
        </tr>
        <tr>
            <td><a href="https://github.com/JdeRobot/RoboticsAcademy/pull/2635">#2635</a></td>
            <td><a href="https://github.com/JdeRobot/RoboticsAcademy/issues/2634">#2634</a></td>
            <td>
                Created a new database entry and added files for the Rescue People Gz Harmonic Exercise<br>
                New "visualisation" and "world" types for Gazebo Sim
            </td>
            <td><a href="https://theroboticsclub.github.io/gsoc2024-Prajyot_Jadhav/blog/2024/coding-period-week-5-6/">Week-5, 6 Blog</a>, 
            <a href="https://theroboticsclub.github.io/gsoc2024-Prajyot_Jadhav/blog/2024/coding-period-week-7/">Week-7 Blog</a>
            </td>
        </tr>
        <tr>
             <td colspan="4"><a href="https://github.com/JdeRobot/RoboticsInfrastructure">Robotics Infrastructure</a></td>
        </tr>
        <tr>
            <td><a href="https://github.com/JdeRobot/RoboticsInfrastructure/pull/402">#402</a></td>
            <td><a href="https://github.com/JdeRobot/RoboticsInfrastructure/issues/401">#401</a></td>
            <td>Updated SDFFormat files of models used in drone exercises to be compatible with new Gazebo Sim</td>
            <td><a href="https://theroboticsclub.github.io/gsoc2024-Prajyot_Jadhav/blog/2024/coding-period-week-3/">Week-3 Blog</a></td>
        </tr>
        <tr>
            <td><a href="https://github.com/JdeRobot/RoboticsInfrastructure/pull/400">#400</a></td>
            <td>-</td>
            <td>Updated launch files for testing new RAM launcher with a dummy client</td>
            <td><a href="https://theroboticsclub.github.io/gsoc2024-Prajyot_Jadhav/blog/2024/coding-period-week-4/">Week-4 Blog</a></td>
        </tr>
        <tr>
            <td><a href="https://github.com/JdeRobot/RoboticsInfrastructure/pull/410">#410</a>, <a href="https://github.com/JdeRobot/RoboticsInfrastructure/pull/419">#419</a>
            </td>
            <td><a href="https://github.com/JdeRobot/RoboticsInfrastructure/issues/409">#409</a>, <a href="https://github.com/JdeRobot/RoboticsInfrastructure/issues/415">#415</a>
            </td>
            <td>New worlds for Rescue People and Follow Road exercises compatible with Gazebo Harmonic</td>
            <td><a href="https://theroboticsclub.github.io/gsoc2024-Prajyot_Jadhav/blog/2024/coding-period-week-5-6/">Week-5, 6 Blog</a></td>
        </tr>
                <tr>
            <td><a href="https://github.com/JdeRobot/RoboticsInfrastructure/pull/412">#412</a>, <a href="https://github.com/JdeRobot/RoboticsInfrastructure/pull/413">#413</a>
            </td>
            <td><a href="https://github.com/JdeRobot/RoboticsInfrastructure/issues/403">#403</a>, <a href="https://github.com/JdeRobot/RoboticsInfrastructure/issues/406">#406</a>
            </td>
            <td>Updated CustomRobots Hooks and .env script for Gazebo Harmonic</td>
            <td><a href="https://theroboticsclub.github.io/gsoc2024-Prajyot_Jadhav/blog/2024/coding-period-week-5-6/">Week-5, 6 Blog</a></td>
        </tr>
                <tr>
            <td><a href="https://github.com/JdeRobot/RoboticsInfrastructure/pull/423">#423</a></td>
            <td><a href="https://github.com/JdeRobot/RoboticsInfrastructure/issues/422">#422</a></td>
            <td>New Aerostack2 launcher for Gazebo Sim; PX4 replaced with Aerostack2 Gazebo Platform</td>
            <td><a href="https://theroboticsclub.github.io/gsoc2024-Prajyot_Jadhav/blog/2024/coding-period-week-7/">Week-7 Blog</a></td>
        </tr>
        <tr>
             <td colspan="4"><a href="https://github.com/JdeRobot/RoboticsApplicationManager">Robotics Application Manager</a>(RAM)</td>
        </tr>
        <tr>
            <td><a href="https://github.com/JdeRobot/RoboticsApplicationManager/pull/136">#136</a></td>
            <td><a href="https://github.com/JdeRobot/RoboticsApplicationManager/issues/135">#135</a></td>
            <td>New RAM launcher for Gazebo Harmonic</td>
            <td><a href="https://theroboticsclub.github.io/gsoc2024-Prajyot_Jadhav/blog/2024/coding-period-week-2/">Week-2 Blog</a> , <a href="https://theroboticsclub.github.io/gsoc2024-Prajyot_Jadhav/blog/2024/coding-period-week-4/">Week-4 Blog</a>
            </td>
        </tr>
        <tr>
            <td><a href="https://github.com/JdeRobot/RoboticsApplicationManager/pull/143">#143</a>, <a href="https://github.com/JdeRobot/RoboticsApplicationManager/pull/148">#148</a>
            </td>
            <td><a href="https://github.com/JdeRobot/RoboticsApplicationManager/issues/142">#142</a>, <a href="https://github.com/JdeRobot/RoboticsApplicationManager/issues/143">#143</a></td>
            <td>Added documentation for creating a new RAM launcher and a guide for using the dummy RAM client</td>
            <td><a href="https://theroboticsclub.github.io/gsoc2024-Prajyot_Jadhav/blog/2024/coding-period-week-8-9/">Week-8, 9 Blog</a>
            </td>
        </tr>
        <tr>
            <td><a href="https://github.com/JdeRobot/RoboticsApplicationManager/pull/138">#138</a></td>
            <td>-</td>
            <td>Modified and created launchers for new Gazebo Sim "visualization" and "world" types<br>
            Updated play, pause, and reset functions for Gazebo Sim
            </td>
            <td><a href="https://theroboticsclub.github.io/gsoc2024-Prajyot_Jadhav/blog/2024/coding-period-week-7/">Week-7 Blog</a> , <a href="https://theroboticsclub.github.io/gsoc2024-Prajyot_Jadhav/blog/2024/coding-period-week-8-9/">Week-8, 9 Blog</a>, <a href="https://theroboticsclub.github.io/gsoc2024-Prajyot_Jadhav/blog/2024/coding-period-week-10/">Week-10 Blog</a>
            </td>
        </tr>
    </tbody>
</table>
<hr>

### Future Work

It has been observed that the newly migrated Rescue People exercise, which uses Gazebo Harmonic, takes significantly longer to load compared to exercises based on Gazebo Classic. Also, the Docker container created from the new Docker files takes more time to close. Future work will involve identifying the cause of these delays and addressing them.

For the Rescue People exercise migrated to Gazebo Harmonic, the reset button does not function as expected. Although the drone's position resets to the initial state, there are issues with entering takeoff mode after a reset. This problem arises because Aerostack2's state machine is not updated when the exercise is reset. Further details can be found in the <a href="https://theroboticsclub.github.io/gsoc2024-Prajyot_Jadhav/blog/2024/coding-period-week-11-12/">Week-11 and Week-12 blog post</a>. Resolving this issue will be a key goal.

The previous Rescue People exercise based on Gazebo Classic has an issue where the gzclient is not launched correctly after the file modifications. It is essential to ensure that older drone-based exercises remain unaffected to provide a fallback option if issues arise with the newly migrated exercise. Identifying the exact cause and resolving this issue is essential.

Robotics-Academy features various types of exercises. The migrated drone-based exercise utilizes Aerostack2, which automatically creates topic bridges. Future work will explore migrating exercises where ROS-to-gz-transport topic bridges need to be created manually.

### Conclusion

Participating in Google Summer of Code has been a highly valuable experience. Working with JdeRobot has significantly expanded my technical skills and understanding of open-source development. GSoC also introduced me to an amazing community at JdeRobot.

I would like to thank Prof. José María Cañas and the JdeRobot admins for providing this opportunity. Special thanks to my mentors, Pedro Arias Pérez, Pawan Wadhwani, Miguel Fernández Cortizas, and Apoorv Garg, for their invaluable guidance and support.
<hr>
