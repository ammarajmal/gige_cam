cmake_minimum_required(VERSION 3.16.3)
project(opencv_cam)

find_package(OpenCV)
include_directories(${OpenCV_INCLUDE_DIRS})
include_directories(include)

if("${CMAKE_SYSTEM_PROCESSOR}" MATCHES "x86_64.*")
  set(SYSTEM_ARCHITECTURE x64)
endif()
if("${CMAKE_SYSTEM_PROCESSOR}" MATCHES "aarch64.*")
  set(SYSTEM_ARCHITECTURE arm64)
endif()

link_directories(lib/${SYSTEM_ARCHITECTURE})

#set(LIB_UNITREE -pthread libunitree_legged_sdk.so lcm)
set(GIGE_CAM libMVSDK.so)
add_executable(cam_gige src/main.cpp)
target_link_libraries(cam_gige ${GIGE_CAM} ${OpenCV_LIBRARIES})


