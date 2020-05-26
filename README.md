# JKK Automotive simulation
This repository contains the simulation of the following vehicles:
- Nissan Leaf test vehicle

The following test environments
- ZalaZone

# Getting started

## Tool requirements
Gazebo 11 is recommended, as we have tested with this version. Also as LIDAR simulation will be extensively used, it is also preferred to build it from source.
- Install Gazebo 11 via Ubuntu pacakges: http://gazebosim.org/tutorials?tut=install_ubuntu&cat=install 
  - One-liner: `sudo apt install ros-$ROS_DISTRO-gazebo11-ros-pkgs`
  - If you want to be 100% sure that your simulation will utilize GPU, install it from source.
- Install Gazebo 11 from source: http://gazebosim.org/tutorials?tut=install_from_source&cat=install 

The following 3rd party packages are required:
- gazebo_ros (mandatory)
- autoware_msgs
- Velodyne Gazebo plugins for the LIDAR simulation. Get it from here, and clone it to your workspace: https://bitbucket.org/DataspeedInc/velodyne_simulator/src/master/
- Hector Gazebo plugins for GPS sensor simulation. Get it from here, and clone it to your workspace (https://github.com/tu-darmstadt-ros-pkg/hector_gazebo)
  - Or install through apt: ```sudo apt install ros-melodic-hector-gazebo-plugins```

Additional requirements:
- szelectricity_common (you can obtain it here: https://github.com/szenergy/szenergy-common, clone it to your workspace)
- nissan_leaf_ros (optional req., you can obtain it here: https://github.com/szenergy/nissan_leaf_ros, clone it to your workspace)

You may also want to check out the __nissan_leaf_ros__ repository, for the real vehicle (optional): https://github.com/szenergy/nissan_leaf_ros This package is optional requirement for visualization purposes.

## Installation steps
Clone this repository to your workspace, and build it (ensure you are at the root of the workspace):
```
catkin build
```
If you build the packages first time, you will need to setup the workspace once again (assuming you are in the root of the workspace):
```
source ./devel/setup.bash
```

Starting fresh, install the Zalazone gazebo models with the following script (this will copy the models into the system gazebo folder):
```bash
./install_zalazone_gazebo.sh
```

# Zalazone simulation with Nissan Leaf loaded
To start the Zalazone simulation, start __gzserver__ with Zalazone loaded:
```
cd zalazone/zalazone_gazebo/sdf
rosrun gazebo_ros gzserver zalazone.sdf
```

Next, load the Nissan Leaf model into the simulation, with the following launch file (this offsets the vehicle with the correct height):
```bash
roslaunch zalazone_gazebo load_nissan_leaf.launch
```
For many applications of ROS, you shall need a static TF tree from __base_link__ and to the sensors. YOu can broadcast this with the following launch file:
```bash
roslaunch nissan_sim_bringup nissanleaf_statictf_launch.simulation.launch
```
Alternatively, if you want to view the vehicle's geometry as well:
```bash
roslaunch nissan_sim_bringup nissan.leaf.staticbringup.ref.sim.launch
```

__Note__: by following these instructions, to see anyithing, you will have to start gzclient separately, like this:
```bash
gzclient
```


Enjoy! An example simulation is shown below:
![alt text](https://github.com/szenergy/jkk-automotive-simulation/blob/master/docs/zalazone_gazebo.jpg "Gazebo example")

# Summary of commands (installation from fresh)
```bash
# Change directory to your workspace's source (e.g. catkin_ws)
cd ~/catkin_ws/src
# Clone workspace
git clone https://github.com/szenergy/jkk-automotive-simulation
# Optionally clone physical description of nissan leaf description
git clone https://github.com/szenergy/nissan_leaf_ros
# Build workspace (in root of workspace)
cd ~/catkin_ws
catkin build
# Start ROS master (separately)
roscore
# Change to jkk-automative source
cd src/jkk-automotive-simulation
# Copy model to .gazebo folder (fresh install)
./install_zalazone_gazebo.sh
# Start Gazebo server
cd zalazone/zalazone_gazebo/sdf
rosrun gazebo_ros gzserver zalazone.sdf
# Source setup.bash when packages are built first time
cd ~/catkin_ws
source ./devel/setup.bash
# Load Nissan Leaf
roslaunch zalazone_gazebo load_nissan_leaf.launch
# Start static TF for simulation AND visualization of vehicle geometry
roslaunch nissan_sim_bringup nissan.leaf.staticbringup.ref.sim.launch
# Start gzclient
gzclient
```

# Summary of system configuration
| Package name            |Version| Req. type   | Source | Web page                                                  |
|-------------------------|-------|-------------|--------|-----------------------------------------------------------|
| Ubuntu                  | 18.04 bionic | Operating-system | system | https://releases.ubuntu.com/18.04.4/ |
| ROS                     | melodic | Mandatory framework | apt    | http://wiki.ros.org/ |
| Gazebo                  | 11.0    | Mandatory tool      | apt    | http://gazebosim.org/ |
| ROS gazebo              | melodic | Mandatory package   | apt    | https://github.com/ros-simulation/gazebo_ros_pkgs          |
| autoware.ai             | 1.13 |Required Framework  | gitlab | https://gitlab.com/autowarefoundation/autoware.ai/autoware |
| Velodyne gazebo plugins | 1.0.9 | Gazebo plugins      | github | https://bitbucket.org/DataspeedInc/velodyne_simulator/src/master/ |
| hector_gazebo_plugins | melodic-devel| GPS plugin | github | https://github.com/tu-darmstadt-ros-pkg/hector_gazebo |
| szelectricity_common| 0.1 | Custom package (organziation)| github | https://github.com/szenergy/szenergy-common |
| nissan_leaf_ros     | 0.1 | Custom package (organization)| github | https://github.com/szenergy/nissan_leaf_ros |


Last modification: 2020.05.25
