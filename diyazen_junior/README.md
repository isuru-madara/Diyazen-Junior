# Diyazen Junior

1. First of all clone this repository to your local machine. 

    ```sh
    $ git clone git@gitlab.com:arimac-robotics/diyazen-junior.git
    ```

2. Install catkin tools in order to build the workspace

    ```sh
    $ sudo apt-get update

    $ sudo apt-get install python-catkin-tools
    ```

3. Install all the dependencies required to run the simulation.

    ```sh
    $ rosdep update

    $ rosdep install --from-paths src --ignore-src --rosdistro=kinetic -y
    ```

4. Build the workspace

    ```sh
    $ catkin build
    ```

    _You should see the directories build, devel, logs alongside with src_. 

5. Source your workspace. First, Navigate to the root of your workspace. 

    ```sh
    $ source /devel/setup.bash
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

8. Most important step- Enjoy! 






