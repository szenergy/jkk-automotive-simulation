# JKK Automotive simulation
This repository contains the simulation of the following vehicles:
- Nissan Leaf test vehicle

The following test environments
- ZalaZone

# Getting started
First time, install the Zalazone gazebo models with the following script (this will copy the models into the system gazebo folder):
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

Last modification: 2020.05.07
