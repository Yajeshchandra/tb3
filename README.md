# TurtleBot3 Navigation in Hospital World

This repository contains the necessary instructions and scripts to run the TurtleBot3 in `hospital.world`, perform SLAM using gmapping, save the generated map, and execute autonomous exploration.

## Prerequisites and Dependencies

```bash
sudo apt-get install ros-noetic-joy ros-noetic-teleop-twist-joy \
ros-noetic-teleop-twist-keyboard ros-noetic-laser-proc \
ros-noetic-rgbd-launch ros-noetic-rosserial-arduino \
ros-noetic-rosserial-python ros-noetic-rosserial-client \
ros-noetic-rosserial-msgs ros-noetic-amcl ros-noetic-map-server \
ros-noetic-move-base ros-noetic-urdf ros-noetic-xacro \
ros-noetic-compressed-image-transport ros-noetic-rqt* ros-noetic-rviz \
ros-noetic-gmapping ros-noetic-navigation ros-noetic-interactive-markers

sudo apt install ros-noetic-turtlebot3-msgs
sudo apt install ros-noetic-turtlebot3
sudo apt-get install ros-noetic-explore-lite
```

## Installation
Download my repository of my workspace

```bash
git clone <repo_url>
```

After downloading the repository, navigate to the turtlebot3_simulations/turtlebot3_gazebo/Dataset/worlds/hospital
Create a models folder and unzip models_part*.zip into it.

## Usage

0. Source the ROS environment and set the environment variables (Do this step for every terminal you open):
```bash
source /opt/ros/noetic/setup.bash
source ~/tb3/devel/setup.bash
export TURTLEBOT3_MODEL=burger
```
1. Launch the Gazebo simulation environment with the TurtleBot3 in the hospital world:
```bash
export GAZEBO_MODEL_PATH=~/tb3/src/turtlebot3_simulations/turtlebot3_gazebo/Dataset/worlds/hospital/models
roslaunch turtlebot3_gazebo turtlebot3_hospital.launch
```
2. Launch the SLAM node to perform mapping of the environment:
```bash
roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping
```
3. Launch the Move Base node:
```bash
roslaunch turtlebot3_navigation move_base.launch
```
4. Launch the exploration node:
```bash
roslaunch explore_lite explore.launch
```
5. Save the map:
```bash
rosrun map_server map_saver -f ~/tb3/src/turtlebot3_simulations/turtlebot3_gazebo/Dataset/worlds/hospital/maps/hospital_map
```
6. Close all the terminals and restart the Gazebo simulation environment:
```bash
export GAZEBO_MODEL_PATH=~/tb3/src/turtlebot3_simulations/turtlebot3_gazebo/Dataset/worlds/hospital/models
roslaunch turtlebot3_gazebo turtlebot3_hospital.launch
```
7. To run the navigation using the saved map:
```bash
roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/tb3/src/turtlebot3_simulations/turtlebot3_gazebo/Dataset/worlds/hospital/maps/hospital_map.yaml
```

## Tutorial Video
[![Tutorial Video]](https://youtu.be/5H19_gXglJ8)

## References
- [TurtleBot3](https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/)
- [ROS Wiki](http://wiki.ros.org/)
- [ROS Navigation](http://wiki.ros.org/navigation)
- [ROS Explore Lite](http://wiki.ros.org/explore_lite)

