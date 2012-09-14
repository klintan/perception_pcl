cmake_minimum_required(VERSION 2.8.3)
project(pcl_conversions)

find_package(catkin REQUIRED COMPONENTS pcl_msgs roscpp sensor_msgs std_msgs)

find_package(PCL REQUIRED COMPONENTS common io)
find_package(Eigen3 REQUIRED)

catkin_package(
  INCLUDE_DIRS include
  CATKIN_DEPENDS pcl_msgs roscpp sensor_msgs std_msgs
  DEPENDS Eigen3 PCL
)

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)

if(CATKIN_ENABLE_TESTING)
  include_directories(
    include
    ${catkin_INCLUDE_DIRS}
    ${PCL_INCLUDE_DIRS}
    ${Eigen3_INCLUDE_DIRS})

  catkin_add_gtest(test_pcl_conversions test/test_pcl_conversions.cpp)
  target_link_libraries(test_pcl_conversions ${catkin_LIBRARIES})
endif()