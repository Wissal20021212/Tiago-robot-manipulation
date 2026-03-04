🚀 ROS2 Navigation & Map Processing – MFJA 3rd Floor

Version ENG : 

👩‍💻 Author
Wissal Mehrez
Robotics Engineering Student – Université Paul Sabatier Toulouse

Specialization: Autonomous Navigation & ROS2 Systems

📌 Project Overview

This project presents a complete ROS2 Navigation2 (Nav2) workflow including:

-Real robot SLAM mapping

-Map extraction and transfer

-Simulation in Gazebo

-Map cleaning & processing

-Robot pose correction

-Environment modification

-Implementation of Keepout zones using Nav2 costmap filters

The project was conducted using the TIAGo robot platform and ROS2.![bb4d2392-7831-4a5e-884c-ac643a1c76d8-ezgif com-cut](https://github.com/user-attachments/assets/024be807-8dc0-4f81-8563-61411d4d70d2)

🛠 Technologies Used

**ROS2**

**Navigation2 (Nav2)**

**SLAM**

**Gazebo**

**RViz**

**TIAGo Robot**

**YAML configuration**

**Costmap filters**

**SSH remote robot control**


🧭 Part 1 – Real Robot Mapping (SLAM)

🔹 Robot Connection

	Ethernet connection

	SSH access to robot

SLAM restart using:

	pal module stop slam
	pal module start slam

🔹 Real-Time Mapping

	rviz2 -d /opt/pal/alum/share/pmb2_2dnav/rviz/navigation.rviz

The map was built incrementally while navigating the MFJA 3rd floor.

Map Saving : 
	
	ros2 run nav2_map_server map_saver_cli -t /map -f /tiago-ws/pal/my_map/mfja_3rd_floor_map_W

Generated:

	map.pgm

	map.yaml

<img width="328" height="714" alt="image" src="https://github.com/user-attachments/assets/fce18e2d-71c5-4b5a-8348-ea2ae069d5a1" />
<img width="367" height="225" alt="image" src="https://github.com/user-attachments/assets/8bc081d5-7240-4b96-b700-71c91ed77b89" />


🧭 Part 2 – Simulation & Navigation in Gazebo

Both file map.pgm et map.yaml are saved in mfja_3rd_floor_map_WM folder

🔹 Launch Gazebo World

	ros2 launch tiago_gazebo tiago_gazebo.launch.py \is_public_sim:=True \ world_name:=mfja_3rd_floor

🔹 Launch Navigation ( Based on the map we exctracted )

For offline navigation in the saved map, make sure that SLAM is closed and load the saved map with tiago_nav_bringup:

	ros2 launch tiago_2dnav tiago_nav_bringup.launch.py \is_public_sim:=True \world_name:=mfja_3rd_floor_map_WM

🧼 Part 3 – Map Cleaning & Optimization
Problem:

Real map contained noise (false obstacles) not present in simulation : 

The robot kept avoiding obstacles on the map that were not present in the real environment. These obstacles were caused by noise detected during real-world navigation.

🔹Solution:

Edited map.pgm using GIMP

Removed noise artifacts

Preserved wall geometry

🔹This improved:

Path planning quality

Costmap reliability

Robot trajectory smoothness

<img width="1168" height="580" alt="image" src="https://github.com/user-attachments/assets/e9720040-002e-4ad7-901b-2d5bb5b3d1ab" />



📍 Part 4 – Robot Initial Pose Correction

Initial robot pose was incorrect due to map origin configuration.

In map.yaml:

	origin: [x, y, 0]

Key discovery:

Positive values caused robot to be outside the map

Correct values had to be negative

Example:

	origin: [-15.2, -76.8, 0]

This demonstrates understanding of:

-Map coordinate frames

-ROS map reference system

🧱 Part 5 – Environment Modification (Gazebo)

Modified simulation world:

-Extracted model from house.world

-Added objects (kitchen table)

-Integrated into mfja_3rd_floor.world

Rebuilt workspace after modification:
	
	colcon build

<img width="370" height="508" alt="image" src="https://github.com/user-attachments/assets/7c7f4ddc-78d5-420d-ad3e-895c659ded43" />

	
