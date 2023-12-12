My job is to emulate [his work](https://github.com/castacks/PX4-fully-actuated.git) and port the code of px4-fully-actuated to `v1.11.3` version.

## Installation

If there is no catkin workspace, you can create a catkin workspace and go to the `src` directory with the following command:

```
mkdir -p catkin_ws/src
cd catkin_ws/src
```

Now clone this repository and all its submodules:

```
git clone https://github.com/Lokleee/PX4-fully-actuated-v1.11.3.git Firmware --recursive
```
Test that everything works fine using the guide on [this page](https://dev.px4.io/master/en/setup/building_px4.html#first-build-using-the-jmavsim-simulator).
Add the environment variable `PX4PATH` to your `.bashrc` file to get global access to the path. For example, if you have used the `catkin_ws` workspace created above, you can do this:

```
echo 'export PX4PATH=$HOME/catkin_ws/src/Firmware' >> ~/.bashrc
```

Now make sure you properly set the Gazebo path to the one in this repo. Add the following to the end of your `.bashrc` file:

```
source /usr/share/gazebo/setup.sh
export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:$PX4PATH:$PX4PATH/Tools/sitl_gazebo
export GAZEBO_PLUGIN_PATH=$PX4PATH/build/px4_sitl_default/build_gazebo:$GAZEBO_PLUGIN_PATH
export GAZEBO_MODEL_PATH=$PX4PATH/Tools/sitl_gazebo/models:$GAZEBO_MODEL_PATH
export GAZEBO_RESOURCE_PATH=$PX4PATH/Tools/sitl_gazebo/worlds:$GAZEBO_RESOURCE_PATH
```

## How to use

The current tilted-hex airframe is defined to have 30 degrees of side tilt. To change the geometry for your airframe, you can modify the definition of the tilted hex or add your own definition. To add the new definition file, please consult the PX4 guides above. To modify our airframe, you can find it [here](https://github.com/Lokleee/PX4-fully-actuated-v1.11.3/blob/v1.11.3-master/src/lib/mixer/MultirotorMixer/geometries/hex_x_tilt.toml).

## Simulation and more

To simulate using Gazebo, you can run the SITL simulation of our UAV using the following command (needs to be executed from the `Firmware` folder):

```
make px4_sitl gazebo_hexa_x_tilt_p
```
