
# Milestone 02: Autonomous Systems Project (Team 24)

## Project Overview
This project implements an **Open Loop Response (OLR)** and **Teleoperation** system for an autonomous vehicle. It integrates a ROS 2 Gazebo simulation with physical hardware (Raspberry Pi and Arduino). The architecture is distributed across specialized packages to handle navigation, locomotion, and system-wide orchestration.

---

## Package Structure & Roles

### 1. `Autonomous_Systems_Project_Team_24`
This is the **Master Orchestration Package**.
* **Launch Files**: Contains the primary launch file that triggers the entire system (Gazebo, OLR node, Teleop node, and the ROS-GZ Bridge).
* **Coordination**: It calls the executables located in the `navigation_pkg`.

### 2. `navigation_pkg`
Contains the core control logic nodes used in this milestone:
* **`olr_node`**: Executes autonomous movement based on parameters (`desired_speed`, `steering`) and prints real-time states (Pose X/Y, Yaw, Velocity) to the terminal.
* **`teleop_node`**: Provides manual control capabilities.

### 3. `locomotion_pkg`
Contains the physical and visual representation of the vehicle:
* **Dynamics & Kinematics**: Mathematical models defining the car's movement.
* **Meshes**: 3D visual files and SDF models (`my_car.sdf`) for the Gazebo environment.

### 4. Future Milestone Files (Neglect for MS2)
The following files are included for future development and are **not active** for this milestone's assessment:
* `controller.py` / `planner.py`
* `serial_bridge_node.py` (The system currently uses the standalone Raspberry Pi bridge script for MS2 hardware communication).

---

## Technical Specifications

### Control Logic & Mapping
The OLR node utilizes ROS 2 parameters to publish `geometry_msgs/Twist` messages. The steering angle for the hardware is calculated as:
$$servoAngle = 90 + (steering \times 45)$$
Where `steering` is a normalized value between **-1.0 (Max Right)** and **1.0 (Max Left)**.

### Communication
* **Simulation**: `ros_gz_bridge` handles the bidirectional data flow between ROS 2 and Gazebo (Cmd_vel and Pose).
* **Hardware**: A serial bridge on the Raspberry Pi communicates with the Arduino at **115200 baud**.

---

## Execution Instructions

### 1. Build the Workspace
```bash
cd ~/auto_ws
colcon build
source install/setup.bash
export ROS_DOMAIN_ID=24
```

### 2. Launch the System
Run the master launch file from the orchestration package:
```bash
ros2 launch Autonomous_Systems_Project_Team_24 Autonomous_Systems_MS_2_Team_24.launch.py desired_speed:=1.2 steering:=0.5
```

---

## Hardware Pin Mapping (Arduino)
* **MG995 Servo**: Digital Pin 9 (PWM)
* **L298N Motor Driver**: Pins 5, 6 (EN), Pins 7, 8, 12, 13 (IN)
* **Power**: Common ground established between Arduino, Raspberry Pi, and external battery packs.

---

> **Note to Evaluator**: The files `controller`, `planner`, and `serial_bridge_node` are preparatory files for Milestone 03 and beyond. For Milestone 02, please refer strictly to the `olr_node` and `teleop_node` within `navigation_pkg`.
