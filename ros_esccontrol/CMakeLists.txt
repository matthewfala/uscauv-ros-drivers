cmake_minimum_required(VERSION 2.8.3)
project(ros_esccontrol)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  i2c_cpp
  std_msgs
  message_generation
)

add_message_files(FILES
		  ESCThrottle.msg)
		  
generate_messages(DEPENDENCIES std_msgs)


## System dependencies are found with CMake's conventions
# find_package(Boost REQUIRED COMPONENTS system)


###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## INCLUDE_DIRS: uncomment this if you package contains header files
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need
catkin_package(
  INCLUDE_DIRS include
  DEPENDS std_msgs
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
# include_directories(include)
include_directories(
   src/lib/PCA9685 ${catkin_INCLUDE_DIRS}
)

add_executable(esccontroller src/controller_sub.cpp src/lib/PCA9685/PCA9685.cpp)
add_dependencies(esccontroller ros_esccontrol_generate_messages_cpp)
target_link_libraries(esccontroller ${catkin_LIBRARIES})


