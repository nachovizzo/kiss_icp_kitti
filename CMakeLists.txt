# MIT License
#
# Copyright (c) 2022 Ignacio Vizzo, Tiziano Guadagnino, Benedikt Mersch, Cyrill
# Stachniss.
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.
cmake_minimum_required(VERSION 3.24)
project(kiss_icp_kitti VERSION 0.2.2 LANGUAGES CXX)

set(ignore ${CATKIN_INSTALL_INTO_PREFIX_ROOT})
set(CMAKE_BUILD_TYPE Release)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

if(EXISTS ${CMAKE_CURRENT_SOURCE_DIR}/../kiss_icp/cpp/kiss_icp/)
  add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../kiss_icp/cpp/kiss_icp ${CMAKE_CURRENT_BINARY_DIR}/kiss_icp)
else()
  message(STATUS "Performing out-of-tree build, fetching KISS-ICP v${CMAKE_PROJECT_VERSION} Release from Github")
  include(FetchContent)
  FetchContent_Declare(
    ext_kiss_icp_core PREFIX kiss_icp_core
    URL https://github.com/PRBonn/kiss-icp/archive/refs/tags/v${CMAKE_PROJECT_VERSION}.tar.gz SOURCE_SUBDIR
        cpp/kiss_icp)
  FetchContent_MakeAvailable(ext_kiss_icp_core)
endif()

find_package(
  catkin REQUIRED
  COMPONENTS geometry_msgs
             nav_msgs
             sensor_msgs
             roscpp
             rosbag
             std_msgs
             tf2
             tf2_ros)
catkin_package()

add_executable(kitti_helper_node src/kitti_helper_node.cpp)
target_include_directories(kitti_helper_node PUBLIC include ${catkin_INCLUDE_DIRS})
target_link_libraries(kitti_helper_node kiss_icp::core ${catkin_LIBRARIES})
install(TARGETS kitti_helper_node RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
