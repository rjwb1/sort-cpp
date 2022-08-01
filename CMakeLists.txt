cmake_minimum_required(VERSION 2.8.3)
project(sortcpp)

## Add support for C++11, supported in ROS Kinetic and newer
add_definitions(-std=c++11)

catkin_package()

find_package(catkin REQUIRED COMPONENTS
  roscpp
)

find_package( OpenCV REQUIRED )
if( OpenCV_FOUND )
list( APPEND ThirdParty_LIBS ${OpenCV_LIBS} )
    include_directories( ${OpenCV_INCLUDE_DIRS} )
endif( OpenCV_FOUND )

include_directories(  
    include
    ${catkin_INCLUDE_DIRS}        
    ${OpenCV_INCLUDE_DIRS}
)

# ==============================================
# Build
# ==============================================

add_executable(
    ${PROJECT_NAME}_test
    src/Hungarian.cpp
    src/KalmanTracker.cpp
    src/main.cpp
)

# ==============================================
# Install
# ==============================================

target_link_libraries(
    ${PROJECT_NAME}_test
    ${catkin_LIBRARIES}
    ${OpenCV_LIBS})

add_dependencies(
    ${PROJECT_NAME}_test
    ${${PROJECT_NAME}_EXPORTED_TARGETS}
    ${catkin_EXPORTED_TARGETS})
