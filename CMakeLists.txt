cmake_minimum_required(VERSION 2.8.3)
project(obot-ros)

## Compile as C++11, supported in ROS Kinetic and newer
# add_compile_options(-std=c++11)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  interactive_markers
  sensor_msgs
  std_msgs
  tf2
)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)
find_package(Eigen REQUIRED)
include_directories(${Eigen_INCLUDE_DIRS})
include_directories(${EIGEN_INCLUDE_DIRS})
option(BUILD_OBOT "Obot nodes" ON)
set(OBOT_INCLUDE_DIR "/usr/include" CACHE PATH "location of obot_messages.h")

## System dependencies are found with CMake's conventions
# find_package(Boost REQUIRED COMPONENTS system)


## Uncomment this if the package has a setup.py. This macro ensures
## modules and global scripts declared therein get installed
## See http://ros.org/doc/api/catkin/html/user_guide/setup_dot_py.html
# catkin_python_setup()

################################################
## Declare ROS messages, services and actions ##
################################################

## To declare and build messages, services or actions from within this
## package, follow these steps:
## * Let MSG_DEP_SET be the set of packages whose message types you use in
##   your messages/services/actions (e.g. std_msgs, actionlib_msgs, ...).
## * In the file package.xml:
##   * add a build_depend tag for "message_generation"
##   * add a build_depend and a exec_depend tag for each package in MSG_DEP_SET
##   * If MSG_DEP_SET isn't empty the following dependency has been pulled in
##     but can be declared for certainty nonetheless:
##     * add a exec_depend tag for "message_runtime"
## * In this file (CMakeLists.txt):
##   * add "message_generation" and every package in MSG_DEP_SET to
##     find_package(catkin REQUIRED COMPONENTS ...)
##   * add "message_runtime" and every package in MSG_DEP_SET to
##     catkin_package(CATKIN_DEPENDS ...)
##   * uncomment the add_*_files sections below as needed
##     and list every .msg/.srv/.action file to be processed
##   * uncomment the generate_messages entry below
##   * add every package in MSG_DEP_SET to generate_messages(DEPENDENCIES ...)

## Generate messages in the 'msg' folder
# add_message_files(
#   FILES
#   Message1.msg
#   Message2.msg
# )

## Generate services in the 'srv' folder
# add_service_files(
#   FILES
#   Service1.srv
#   Service2.srv
# )

## Generate actions in the 'action' folder
# add_action_files(
#   FILES
#   Action1.action
#   Action2.action
# )

## Generate added messages and services with any dependencies listed here
# generate_messages(
#   DEPENDENCIES
#   sensor_msgs#   std_msgs
# )

################################################
## Declare ROS dynamic reconfigure parameters ##
################################################

## To declare and build dynamic reconfigure parameters within this
## package, follow these steps:
## * In the file package.xml:
##   * add a build_depend and a exec_depend tag for "dynamic_reconfigure"
## * In this file (CMakeLists.txt):
##   * add "dynamic_reconfigure" to
##     find_package(catkin REQUIRED COMPONENTS ...)
##   * uncomment the "generate_dynamic_reconfigure_options" section below
##     and list every .cfg file to be processed

## Generate dynamic reconfigure parameters in the 'cfg' folder
# generate_dynamic_reconfigure_options(
#   cfg/DynReconf1.cfg
#   cfg/DynReconf2.cfg
# )

###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## INCLUDE_DIRS: uncomment this if your package contains header files
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need
catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES unhuman-ros
#  CATKIN_DEPENDS interactive_markers sensor_msgs std_msgs tf2
#  DEPENDS system_lib
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
include_directories(
# include
  ${catkin_INCLUDE_DIRS}
)

## Declare a C++ library
# add_library(${PROJECT_NAME}
#   src/${PROJECT_NAME}/unhuman-ros.cpp
# )

## Add cmake target dependencies of the library
## as an example, code may need to be generated before libraries
## either from message generation or dynamic reconfigure
# add_dependencies(${PROJECT_NAME} ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

add_executable(${PROJECT_NAME}_wrist_marker src/wrist_marker.cpp)
set_target_properties(${PROJECT_NAME}_wrist_marker PROPERTIES OUTPUT_NAME wrist_marker PREFIX "")
add_dependencies(${PROJECT_NAME}_wrist_marker ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(${PROJECT_NAME}_wrist_marker ${catkin_LIBRARIES})

add_executable(${PROJECT_NAME}_joystick src/joystick.cpp)
set_target_properties(${PROJECT_NAME}_joystick PROPERTIES OUTPUT_NAME joystick PREFIX "")
add_dependencies(${PROJECT_NAME}_joystick ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(${PROJECT_NAME}_joystick ${catkin_LIBRARIES})

add_executable(${PROJECT_NAME}_joystick_arm src/joystick_arm.cpp)
set_target_properties(${PROJECT_NAME}_joystick_arm PROPERTIES OUTPUT_NAME joystick_arm PREFIX "")
add_dependencies(${PROJECT_NAME}_joystick_arm ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(${PROJECT_NAME}_joystick_arm ${catkin_LIBRARIES})

add_executable(${PROJECT_NAME}_joystick_goal src/joystick_goal.cpp)
set_target_properties(${PROJECT_NAME}_joystick_goal PROPERTIES OUTPUT_NAME joystick_goal PREFIX "")
add_dependencies(${PROJECT_NAME}_joystick_goal ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(${PROJECT_NAME}_joystick_goal ${catkin_LIBRARIES})

add_executable(${PROJECT_NAME}_joystick_arm_task src/joystick_arm_task.cpp)
set_target_properties(${PROJECT_NAME}_joystick_arm_task PROPERTIES OUTPUT_NAME joystick_arm_task PREFIX "")
add_dependencies(${PROJECT_NAME}_joystick_arm_task ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(${PROJECT_NAME}_joystick_arm_task ${catkin_LIBRARIES})

add_executable(${PROJECT_NAME}_joint_to_actuator src/joint_to_actuator.cpp)
set_target_properties(${PROJECT_NAME}_joint_to_actuator PROPERTIES OUTPUT_NAME joint_to_actuator PREFIX "")
add_dependencies(${PROJECT_NAME}_joint_to_actuator ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(${PROJECT_NAME}_joint_to_actuator ${catkin_LIBRARIES})

add_executable(${PROJECT_NAME}_joint_to_motor_data src/joint_to_motor_data.cpp)
set_target_properties(${PROJECT_NAME}_joint_to_motor_data PROPERTIES OUTPUT_NAME joint_to_motor_data PREFIX "")
add_dependencies(${PROJECT_NAME}_joint_to_motor_data ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(${PROJECT_NAME}_joint_to_motor_data ${catkin_LIBRARIES} rt pthread)

add_executable(${PROJECT_NAME}_actuator_to_motor src/actuator_to_motor.cpp)
set_target_properties(${PROJECT_NAME}_actuator_to_motor PROPERTIES OUTPUT_NAME actuator_to_motor PREFIX "")
add_dependencies(${PROJECT_NAME}_actuator_to_motor ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(${PROJECT_NAME}_actuator_to_motor ${catkin_LIBRARIES} motor_manager)

add_executable(${PROJECT_NAME}_motor_data_echo src/motor_data_echo.cpp)
set_target_properties(${PROJECT_NAME}_motor_data_echo PROPERTIES OUTPUT_NAME motor_data_echo PREFIX "")
add_dependencies(${PROJECT_NAME}_motor_data_echo ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(${PROJECT_NAME}_motor_data_echo ${catkin_LIBRARIES} rt pthread)

find_package(realtime-rbdl PATHS /home/lee/unhuman/realtime-rbdl/build/artifacts)
find_package(RBDL)

if(realtime-rbdl_FOUND AND rbdl_FOUND) 
  add_executable(${PROJECT_NAME}_realtime src/realtime.cpp)
  set_target_properties(${PROJECT_NAME}_realtime PROPERTIES OUTPUT_NAME realtime PREFIX "")
  add_dependencies(${PROJECT_NAME}_realtime ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
  target_link_libraries(${PROJECT_NAME}_realtime ${catkin_LIBRARIES} realtime-rbdl rbdl)
  target_include_directories(${PROJECT_NAME}_realtime PUBLIC ${RBDL_INCLUDE_DIR} ${EIGEN3_INCLUDE_DIR})
else()
  message("Couldn't find realtime-rbdl or rbdl")
endif()

if(BUILD_OBOT)
  add_subdirectory(src/obot)
endif()

#############
## Install ##
#############

# all install targets should use catkin DESTINATION variables
# See http://ros.org/doc/api/catkin/html/adv_user_guide/variables.html

## Mark executable scripts (Python etc.) for installation
## in contrast to setup.py, you can choose the destination
# catkin_install_python(PROGRAMS
#   scripts/my_python_script
#   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark executables for installation
## See http://docs.ros.org/melodic/api/catkin/html/howto/format1/building_executables.html
# install(TARGETS ${PROJECT_NAME}_node
#   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark libraries for installation
## See http://docs.ros.org/melodic/api/catkin/html/howto/format1/building_libraries.html
# install(TARGETS ${PROJECT_NAME}
#   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   RUNTIME DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION}
# )

## Mark cpp header files for installation
# install(DIRECTORY include/${PROJECT_NAME}/
#   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
#   FILES_MATCHING PATTERN "*.h"
#   PATTERN ".svn" EXCLUDE
# )

## Mark other files for installation (e.g. launch and bag files, etc.)
# install(FILES
#   # myfile1
#   # myfile2
#   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
# )

#############
## Testing ##
#############

## Add gtest based cpp test target and link libraries
# catkin_add_gtest(${PROJECT_NAME}-test test/test_unhuman-ros.cpp)
# if(TARGET ${PROJECT_NAME}-test)
#   target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME})
# endif()

## Add folders to be run by python nosetests
# catkin_add_nosetests(test)
