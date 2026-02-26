# CTZ UAV Simulation

## Installation

```
curl https://ctu-mrs.github.io/ppa-stable/add_ros_ppa.sh | bash
sudo apt install ros-noetic-desktop-full
curl https://ctu-mrs.github.io/ppa-stable/add_ppa.sh | bash
sudo apt install ros-noetic-mrs-msgs ros-noetic-mrs-uav-px4-api ros-noetic-px4 ros-noetic-mavlink-sitl-gazebo ros-noetic-mavros-msgs ros-noetic-mrs-gazebo-common-resources ros-noetic-mrs-uav-testing ros-noetic-mrs-uav-gazebo-testing
```

## Shell Additions
```
cd uav_shell_additions
cp -r etc/uav_ws/ /etc/
cp -r  usr/bin/. /usr/bin/
```
## Start the Gazebo simulator

To start the example Gazebo world call:
```
roslaunch ctz_uav_simulation gazebo_sim.launch world_name:=grass_plane.world gui:=true
```

## Spawning the UAVs
```
rosservice call /uav_spawner/spawn "1 --x500 --enable-rangefinder"

```

To display the basic use manual for the spawner, call the service with the argument  --help

```
rosservice call /uav_spawner/spawn " --x500 --help"
```

Multiple vehicles may be spawned with one service call:
```
rosservice call /uav_spawner/spawn "1 2 3 4 5 --t650 --enable-bluefox-camera --enable-rangefinder"
```

The default parameters of some components may be reconfigured by adding param:=value after the component keyword. Multiple params may be used at the same time:
```
rosservice call /uav_spawner/spawn "1 --x500 --enable-rangefinder --enable-ouster model:=OS0-32 use_gpu:=True horizontal_samples:=128 update_rate:=10"
```