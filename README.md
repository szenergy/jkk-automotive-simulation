# JKK Automotive simulation
This repository contains the simulation of the following vehicles:
- Nissan Leaf test vehicle

The following test environments
- ZalaZone

# Getting started

## Tool requirements
Gazebo 11 is recommended, as we have tested with this version. Also as LIDAR simulation will be extensively used, it is also preferred to build it from source.
- Install Gazebo 11 via Ubuntu pacakges: http://gazebosim.org/tutorials?tut=install_ubuntu&cat=install
- Install Gazebo 11 from source: http://gazebosim.org/tutorials?tut=install_from_source&cat=install

The following 3rd party packages are required:
- gazebo_ros (mandatory)

Additional requirements:
- szelectricity_common (you can obtain it here: https://github.com/szenergy/szenergy-common, clone it to your workspace)

You may also want to check out the __nissan_leaf_ros__ repository, for the real vehicle (optional): https://github.com/szenergy/nissan_leaf_ros

## Installation steps

Starting fresh, install the Zalazone gazebo models with the following script (this will copy the models into the system gazebo folder):
```bash
./install_zalazone_gazebo.sh
```
To start the Zalazone simulation, start __gzserver__ with Zalazone loaded:
```
cd zalazone/zalazone_gazebo/sdf
rosrun gazebo_ros gzserver zalazone.sdf
```

# Load Nissan Leaf into Zalazone
Next, load the Nissan Leaf model into the simulation, with the following launch file (this offsets the vehicle with the correct height):
```bash
roslaunch zalazone_gazebo load_nissan_leaf.launch
```

Enjoy! An example simulation is shown below:
![alt text](https://github.com/szenergy/jkk-automotive-simulation/blob/master/docs/zalazone_gazebo.jpg "Gazebo example")

Last modification: 2020.05.25
