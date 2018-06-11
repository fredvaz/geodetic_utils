cmake_minimum_required(VERSION 2.8.3)
project(geodetic_utils)

## Compile as C++11, supported in ROS Kinetic and newer
add_compile_options(-std=c++11)

## Find catkin macros and libraries
find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  sensor_msgs
  geometry_msgs
  tf
)
find_package(cmake_modules REQUIRED)
find_package(Eigen REQUIRED)

## Generate added messages and services
generate_messages(
  DEPENDENCIES
  std_msgs
)

## Declare a catkin package
catkin_package(
  INCLUDE_DIRS
    include
  CATKIN_DEPENDS
    roscpp
    rospy
    std_msgs
  DEPENDS
    Eigen

# LIBRARIES aqua_gps_localization
)


###########
## Build ##
###########

include_directories(
  ${catkin_INCLUDE_DIRS}
  ${PROJECT_SOURCE_DIR}/include
  ${Eigen_INCLUDE_DIRS}
)

add_executable(
  set_gps_reference_node src/set_gps_reference_node.cpp
)

target_link_libraries(
  set_gps_reference_node
  ${catkin_LIBRARIES}
)

add_executable(
  gps_to_pose_conversion_node src/gps_to_pose_conversion_node.cpp
)

target_link_libraries(
  gps_to_pose_conversion_node
  ${catkin_LIBRARIES}
)

catkin_install_python(PROGRAMS
  src/euler_radians_to_degrees.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
