cmake_minimum_required(VERSION 2.8.3)
project(sbpl_path)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_LIST_DIR}/cmake")

find_package(PkgConfig REQUIRED)
find_package(catkin REQUIRED COMPONENTS
  roscpp
  geometry_utils
  parameter_utils
  sensor_msgs
  geometry_msgs
  nav_msgs
  quadrotor_msgs
  rosgraph_msgs
  tf2_ros
)

catkin_package(
  #INCLUDE_DIRS include
  LIBRARIES ${PROJECT_NAME}
  CATKIN_DEPENDS roscpp geometry_utils tf2_ros
)

pkg_check_modules(SBPL REQUIRED sbpl)

include_directories(include
  ${catkin_INCLUDE_DIRS}
  ${SBPL_INCLUDE_DIRS}
)

link_directories(
  ${catkin_LIBRARY_DIRS}
  ${SBPL_LIBRARY_DIRS}
)

add_definitions(
  ${catkin_DEFINITIONS}
)

add_library(${PROJECT_NAME}
  src/sbpl_path.cpp
)

target_link_libraries(${PROJECT_NAME}
  ${catkin_LIBRARIES}
)

add_dependencies(${PROJECT_NAME}
  quadrotor_msgs_generate_messages_cpp
)

add_executable(${PROJECT_NAME}_node
  src/${PROJECT_NAME}.cpp
)

set_target_properties(${PROJECT_NAME}_node
  PROPERTIES OUTPUT_NAME ${PROJECT_NAME}
)

target_link_libraries(${PROJECT_NAME}_node
  ${PROJECT_NAME}
  ${SBPL_LIBRARIES}
)


install(TARGETS ${PROJECT_NAME} ${PROJECT_NAME}_node
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h"
)
