# Diyazen Junior Demonstration

## System Requirements
 - Ubuntu 16.04 Xnenial 
 - Nvidia graphics (for Gazebo)

## ROS Installation

1. Setup your computer to accept software from packages.ros.org

    ```sh
    sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
    ```


2. Set up your keys
(if you haven't already installed curl)

    ```sh
    sudo apt install curl
    ```
    ```sh 
     curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
    ```

 3. Update Debian indexes.

    ```sh
    sudo apt-get update
    ```

 4. Install ROS
    ```sh
    sudo apt-get install ros-kinetic-desktop-full
    ```
 5. Setup environment variables

    ```sh
    echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
    ```
    ```sh
    source ~/.bashrc
    ```
    _try running `roscore` command in a new BASH terminal to check whether everything is ok so far._

6. Installing dependencies for building ROS packages
    ```sh
    sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential
    ```

 7. Initialise rosdep 
    ```sh 
    sudo apt install python-rosdep
    ```
    ```sh
    sudo rosdep init
    ```
    ```sh
    rosdep update
    ```

   
    

## Gazebo Installation 

 - Gazebo is the 3D simulator that will be used in this demonstration.
 - Since we have done a full desktop installation of ROS, we should have
   standalone Gazebo software running.
 - Check it by running `gazebo` in a new shell. The GUI might take a
   while to load up.
 - In case you have skipped gazebo installation, Install it using, 
   ```sh
   sudo apt-get install gazebo7
   ```
   Now we're ready to install gazebo ROS packages. 
   ```sh
   sudo apt-get install ros-kinetic-gazebo-ros-pkgs ros-kinetic-gazebo-ros-control
   ```

## Setup Catkin tools
We'll be using catkin tools as the build system for our ROS project. Catkin is a wrapper around CMake and it is also responsible for workspace management. 
   ```sh
   sudo apt-get install python-catkin-tools
   ```


## Create a Catkin workspace
We will create a workspace for our project. Navigate to a suitable directory and start creating the workspace file structure.  
```sh
mkdir -p diyazen_junior_ws/src
```
This will create out `src` folder where all ROS packages reside. 
Navigate into `src` and initialise the directory as a Catkin workspace
```sh
cd diyazen_junior_ws/src
catkin_init_workspace 
```
If everything went well, you will have created a symlink inside `src` folder for a top-level `CMakeLists.txt`.



##  Getting started with Diyazen Junior Package
This is a metapackage for adding Diyazen Junior to your project. 

1. First of all clone this repository to your local workspace package level (inside the src directory). 

    ```sh
    git clone https://github.com/isuru-madara/Diyazen-Junior.git
    ```

2. Install all the system dependencies required to run the simulation.

    ```sh
    rosdep update
    ```
    Navigate back to the root of the workspace
    
    ```sh
    cd ../
    ```
    
    ```sh
    rosdep install --from-paths src --ignore-src --rosdistro=kinetic -y
    ```
    At this point rosdep will install <u>almost</u> all dependencies required to run the simulation. However, it might not have keys for all the Debian binaries that is needed for the simulation. For example, it might be missing the package `gmapping` which we will later user for SLAM. Note down all the missing packages reported by rosdep and install them manually using `apt-get` as follows,
    ```sh
    sudo apt-get install ros-kinetic-gmapping
    ```
    Run the above command for all the other missing packages. 

    Alternatively, there is a script included in this repository which installs commonly missing dependencies. 
    First give the file neccessary permission. 
    ```sh
    sudo chmod +x diyazen-junior/diyazen_junior/install_deps.sh
    ````
    And simply run the script. 
    ```sh
    source diyazen-junior/diyazen_junior/install_deps.sh
    ```
3. Build the workspace
    
    Navigate to the base of the catkin workspace. This directory should only contain `src` as of now. 
    ```sh
    catkin build
    ```

    _You should see the directories build, devel, logs alongside with src_ 

5. Source your workspace. First, Navigate to the root of your workspace. 

    ```sh
    $ source devel/setup.bash
    ```

6. Start the mapping demo using Diyazen Junior 

    ```sh
    $ roslaunch diyazen_navigation gazebo_mapping_test.launch
    ```

7. Start the keyboard teleoperation node to manually control the robot.

    ```sh
    $ roslaunch diyazen_teleop keyboard_teleop.launch 
    ```

    _In case you happen to have a Logitech F710 or an Xbox 360 controller handy, you could use that instead!_

8. Most important step- Enjoy!!
