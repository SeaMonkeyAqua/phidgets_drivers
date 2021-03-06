cmake_minimum_required(VERSION 2.8.3)
project(phidgets_ik)

find_package(catkin REQUIRED COMPONENTS geometry_msgs nodelet phidgets_api roscpp sensor_msgs std_msgs std_srvs tf)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES phidgets_ik
  CATKIN_DEPENDS geometry_msgs nodelet phidgets_api roscpp sensor_msgs std_msgs std_srvs tf
)

include_directories(include ${catkin_INCLUDE_DIRS})

add_library(phidgets_ik src/ik_ros_i.cpp)

add_executable(phidgets_ik_node src/phidgets_ik_node.cpp)

add_dependencies(phidgets_ik ${catkin_EXPORTED_TARGETS})
add_dependencies(phidgets_ik_node ${catkin_EXPORTED_TARGETS})

target_link_libraries(phidgets_ik ${catkin_LIBRARIES})
target_link_libraries(phidgets_ik_node ${catkin_LIBRARIES} phidgets_ik)

install(TARGETS phidgets_ik phidgets_ik_node
   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY include/${PROJECT_NAME}/
   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
   FILES_MATCHING PATTERN "*.h"
)
