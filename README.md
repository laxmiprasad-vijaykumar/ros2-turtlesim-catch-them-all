# ros2-turtlesim-catch-them-all
# ROS 2 Turtlesim – Catch Them All

This project implements an autonomous robotics simulation using ROS 2, where a master turtle detects, tracks, and “captures” dynamically spawned turtles in a 2D environment.

The system demonstrates core ROS 2 concepts such as nodes, topics, services, custom interfaces, parameters, and launch-based execution.

---

## 🚀 Project Overview

- A master turtle navigates the environment autonomously  
- Multiple turtles are spawned dynamically  
- The controller selects a target (closest or first)  
- The turtle moves toward the target using a control loop  
- Once reached, a service is called to remove the target  

---

## ⚙️ System Architecture

### Nodes
- `turtle_controller` → controls movement and decision making  
- `turtle_spawner` → spawns and removes turtles  
- `turtlesim_node` → simulation environment  

---

### Topics
- `/turtle1/pose` → current position of the robot  
- `/turtle1/cmd_vel` → velocity commands  
- `/alive_turtles` → list of active turtles  

---

### Services
- `/spawn` → create new turtles  
- `/kill` → remove turtles  
- `/catch_turtle` → custom service for capture logic  

---

### Custom Interfaces
- `Turtle.msg` → stores turtle name and pose  
- `TurtleArray.msg` → list of turtles  
- `CatchTurtle.srv` → request to remove a turtle  

---

## 🧠 Core Logic

- Target selection:
  - closest turtle OR first turtle (parameter-based)
- Navigation:
  - Proportional (P) control for movement  
- System behavior:
  - Continuous spawn → detect → navigate → capture loop  

---

## ⚙️ Parameters

Configured via YAML file:

- `spawn_frequency` → rate of spawning turtles  
- `turtle_name_prefix` → naming pattern  
- `catch_closest_turtle_first` → selection strategy  

---

## ▶️ How to Run

```bash
cd ~/ros2_ws
colcon build
source install/setup.bash

ros2 launch my_robot_bringup turtlesim_catch_them_all.launch.xml
