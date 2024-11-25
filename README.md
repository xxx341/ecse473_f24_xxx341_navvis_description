# Navvis Description Package

This package provides the robot description files for the Navvis robot, including models, sensor integrations, and simulation configurations. It is designed for visualization in RViz, supporting both URDF and XACRO formats.

---

## Features

- Modular robot model using **URDF** and **XACRO**.
- Integration with **Velodyne VLP-16 LIDAR** for point cloud generation.
- Compatibility with **Gazebo simulation** and **RViz visualization**.
- Customizable for different configurations and sensor placements.

---

## Package Contents

### Directory Structure
navvis_description/
├── CMakeLists.txt	# Build system configuration
├── package.xml	# ROS package manifest
├── launch/		# Launch files for RViz and Gazebo
    └── display.launch
├── config/		# RViz configuration files
│   └── config.rviz
├── urdf/		# Contains URDF and XACRO files for the robot
│   ├── robot.urdf
│   └── robot.xacro
└── README.md


### Key Files
- **`robot.xacro`**: Main XACRO file defining the robot model.
- **`launch/display.launch`**: Launch file for RViz visualization.
- **`config/config.rviz`**: RViz configuration file for the robot.

---

## Installation

### Prerequisites
Ensure that you have the following installed:
- **ROS Noetic** or another compatible ROS version.
- Required dependencies (see below).

### Clone and Build
1. Clone this repository into your ROS workspace:
   ```bash
   cd ~/catkin_ws/src
   git clone <repository_url>
2. Build the workspace:
   ```bash
   cd ~/catkin_ws
   catkin_make
3. Source the workspace:
   ```bash
   source ~/catkin_ws/devel/setup.bash
  
---
 
## Usage

### Visualize the Robot in RViz
1. **Using the `joint_state_publisher_gui`** (default):
   To visualize the robot with the GUI sliders for joint state adjustments, run:
   ```bash
   roslaunch navvis_description display.launch
   ```
   The **`joint_state_publisher_gui`** will automatically be launched.
2. Without the **`joint_state_publisher_gui`**: To use the regular **`joint_state_publisher`** instead of the GUI, run:
     ```bash
   roslaunch navvis_description display.launch use_joint_state_publisher_gui:=false

---

## Launch File Details
- **`display.launch`**:
  - Loads the robot description into the parameter server.
  - Launches **RViz** to visualize the robot.
  - Conditionally launches either the **`joint_state_publisher_gui`** or the **`joint_state_publisher`**, based on the **`use_joint_state_publisher_gui`** argument.
  - Default behavior: Launches with **`joint_state_publisher_gui`**.


---

## Dependencies
The package depends on the following ROS packages:
- **`gazebo_plugins`**: Provides Gazebo simulation plugins.
- **`velodyne_description`**: Velodyne LIDAR URDF/XACRO files.
- **`geometry_msgs`**: ROS messages for geometric primitives.
- **`rviz`**: Visualization tool.
- **`sensor_msgs`**: ROS messages for sensors (e.g., LIDAR).
- **`urdf`**: Tools for handling URDF robot models.
- **`xacro`**: Macro processing for URDF generation.

Install missing dependencies using:
```bash
sudo apt install ros-noetic-<package_name>
```

---

## Testing

### Validate the URDF
1. Generate the URDF from the XACRO file:
   ```bash
   rosrun xacro xacro urdf/robot.xacro > robot.urdf
2. Validate the URDF file:
   ```bash
   check_urdf robot.urdf
   
### View Transformations
Ensure the robot’s transforms are correctly published:
   ```bash
   rostopic echo /tf

### Test Sensor Outputs
1. Check that the LIDAR topics are publishing:
   ```bash
   rostopic list
2. Inspect the LIDAR data:
   ```bash
   rostopic echo /laser_horiz/packets
   ```







