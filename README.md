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
	
	ros2 run nav2_map_server map_saver_cli -t /map -f /home/pal/my_map

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

	
