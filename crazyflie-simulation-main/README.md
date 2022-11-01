# IMAV DRONE RACING COMPETITION

Hi! welcome to the IMAV drone racing competition simulation repo.

Currently it contains low resolution meshes based on the design of the actual [crazyflie 2.1](https://www.bitcraze.io/products/crazyflie-2-1/) but heavily simplified to contain as little vertices as possible, so it can be used to simulate a lot of them!

## Content

Currently contains:
* Meshes
    * Blender files
    * STL files
* [Webots](https://cyberbotics.com/) simulation files
    * Currently with velocity control fixed height and firmware python bindings
    * Camera and multiranger sensors
    * All gates and obstacles located based on the previous yer competition
    * Twon environment are provided, A world has gates with aruco markers, and the other one the gates without the aruco markers. The former can be used for training the algorithms, and the later can be used to be as close as possible o the competition environment.
    * The .dae files of the gates are provided as well
* [Gazebo ignition](https://ignitionrobotics.org/) 
    * sdf files
    * no control yet

# Webots

Install webots from the [cyberbotics' website](https://cyberbotics.com/). We use version 2022a version.

Then just run the following

    cd crazyflie-simulation-main
    
if you want to run the have the environment with the aruco markers on the gates, run the following command:

    webots webots/worlds/crazyflie_world_aruco.wbt

otherwise, if you want to have the gates without any marker, run the bellow command:

    webots webots/worlds/crazyflie_world.wbt


## Python controllervbn
Go into the crazyflie-simulation-main/controllers/ folder and run the following:

    swig -python pid_controller.i
    python3 setup.py build_ext --inplace

Change controller in crazyflie robot model to crazyflie_controller_py to try it out. 

## Firmware python bindings
As of this [Pull request in the Crazyflie firmware repo](https://github.com/bitcraze/crazyflie-firmware/pull/1021) it is possible to use the python bindings of the controllers of the actual crazyflie controller directly in webots.

Go the crazyflie-firmware directory in a terminal and write:

    make bindings_python

Change the controller in the crazyflie robot model in webots to crazyflie_controller_py_firmware_pid, and adjust the following line to point to your crazyflie-firmware repo:

    sys.path.append('../../../../../C/crazyflie-firmware')

Press play with the simulator and use your keyboard to  control it 

# Ignition Gazebo

*Just mind that this model does not fly properly yet.* 

1- First install ignition gazebo: https://ignitionrobotics.org/docs/fortress/install

2- Clone this repo: 
    git clone https://github.com/bitcraze/crazyflie_simulation.git

3- Put this repo in your ~/.bashrc and source it in your terminal

    export IGN_GAZEBO_RESOURCE_PATH="path/to/crazyflie-simulation/gazebo-ignition/"

4- Try out the crazyflie world with: 
    ign gazebo crazyflie_world.sdf

5- Spin motors and take off

    ign topic -t /crazyflie/gazebo/command/motor_speed --msgtype ignition.msgs.Actuators -p 'velocity:[2500,2500,2500,2500]'



## Measurements Crazyflie Assembly

The location of the parts

* Propeller origin from center (0.031, 0.031, 0.022) m
    * Mirrored in the x and y axis
* Motor mount + motor mounts (0.031, 0.031, 0.014) m
    * Mirrored in the x and y axis
* Body origin height from center ( 0, 0, 0.015) m
* Battery holder height ( 0, 0,0.025) m
* Battery height (0,0,0.02) m
* Pin headers (0, 0.011, 0.014) m
    * Mirrored in the y axis