COURSE: MCTR1002-AUTONOMOUS SYSTEM - TEAM 24
--- PROJECT OVERVIEW ---
This project involves the development of a car-like autonomous vehicle simulated within the ROS 2 Humble and Gazebo environments. The primary objective is to implement an Ackermann-steered platform capable of precise teleoperation and real-time position feedback.

--- VEHICLE ARCHITECTURE & COMPONENTS ---

MECHANICAL DESIGN (ACKERMANN STEERING)
The vehicle mimics real-world automotive kinematics using Ackermann geometry.

Front System: Utilizes a Servo Motor to control the steering angle of the front wheels.

Rear System: Powered by a DC Motor providing longitudinal drive and velocity.

Turning Logic: Ensures all wheels follow a common turning center to prevent tire slip during maneuvers.

PERCEPTION SYSTEM

Vision-Based: The vehicle is designed to perceive its environment primarily through a Camera-based system.

CONTROL & COMMUNICATION

Custom ROS Node: A specialized Python node translates keyboard inputs into speed and steering commands.

Hardware Interface: In the physical build, a Raspberry Pi  communicates with an Arduino via USB Serial.

Open-Loop Testing: The Arduino manages the motor drivers using fixed PWM signals for hardware validation.

FEEDBACK LOOP

Odometry Tracking: The system subscribes to the vehicle's odometry data to monitor real-time (x, y) coordinates.

Validation: This ensures the "Act" command (movement) matches the "Sense" data (location).

--- SYSTEM SETUP (.bashrc Aliases) ---

alias gazebo: Cleans old processes and starts Gazebo with a forced reset.

alias bridge: Establishes the communication link for Twist and Odometry data.

alias move: Clears the ROS daemon and launches the Teleoperation validation node.

--- EXECUTION FLOW ---

Start Simulation: Type 'gazebo' in the first terminal.

Link Communication: Type 'bridge' in the second terminal.

Launch Controller: Type 'move' in the third terminal to drive the vehicle.

--- VALIDATION NODE LOGIC ---

Control Mapping: W/A/S/D/X keys manage velocity and steering angle parameters.

Performance: Position data is logged at a frequency of 1Hz to maintain terminal clarity.

Safety: An emergency shutdown function stops the vehicle instantly upon exiting (Ctrl+C).

Parameters: The system utilizes 'rosparam' via launch files to define initial and desired speeds.

--- HARDWARE CONFIGURATION ---

Microcontrollers: Raspberry Pi for high-level processing; Arduino for low-level motor control.

Motor Drivers: Integrated to handle the power requirements of the DC drive motors.

Chassis Integration: Components are selected for a compact footprint to fit within the vehicle frame.