cmake_minimum_required(VERSION 2.8.3)
project(braitenberg_local_plannter)

set(CMAKE_CXX_FLAGS "-std=c++11")

find_package(catkin REQUIRED
  COMPONENTS
  roscpp
  costmap_2d
  nav_core
  geometry_msgs
  tf2
  tf2_ros
  pluginlib
  )

catkin_package(
  LIBRARIES braitenberg_local_plannter
  CATKIN_DEPENDS
    roscpp
    costmap_2d
    nav_core
    geometry_msgs
    tf2
    tf2_ros
    pluginlib
)

###########
## Build ##
###########
include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)

add_library(braitenberg_local_plannter src/braitenberg_local_plannter.cpp)
target_link_libraries(braitenberg_local_plannter ${catkin_LIBRARIES})


#############
## Install ##
#############
install(TARGETS braitenberg_local_plannter
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
)

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  PATTERN ".svn" EXCLUDE
)

install(FILES blp_plugin.xml
    DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)
