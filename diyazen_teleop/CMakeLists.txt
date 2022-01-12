cmake_minimum_required(VERSION 2.8.3)
project(diyazen_teleop)

## Find catkin macros and libraries
find_package(catkin REQUIRED COMPONENTS
  geometry_msgs
  joy
  roscpp
  std_msgs
  move_base_msgs
  actionlib
  actionlib_msgs
)

###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
catkin_package()

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
include_directories(
# include
  ${catkin_INCLUDE_DIRS}
)

add_executable(diyazen_teleop_joy src/diyazen_joy.cpp)
target_link_libraries(diyazen_teleop_joy ${catkin_LIBRARIES})

