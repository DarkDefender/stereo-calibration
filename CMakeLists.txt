cmake_minimum_required(VERSION 2.8.11)
project(CALIB_CAM)

if(APPLE)
	link_directories(/usr/local/opt/opencv3/share/OpenCV/3rdparty/lib/ /usr/local/opt/opencv3/lib)
endif()

set(CMAKE_INCLUDE_CURRENT_DIR ON)

#find_package(OpenCV REQUIRED)
include(FindPkgConfig)
pkg_search_module(OPENCV REQUIRED opencv)
include_directories(${OPENCV_INCLUDE_DIRS})

add_executable(calibrate calib_intrinsic.cpp popt_pp.h)
target_link_libraries(calibrate ${OPENCV_LIBRARIES} "-lpopt")

add_executable(read read_images.cpp)
target_link_libraries(read ${OPENCV_LIBRARIES} "-lpopt")

add_executable(calibrate_stereo calib_stereo.cpp)
target_link_libraries(calibrate_stereo ${OPENCV_LIBRARIES} "-lpopt")

add_executable(undistort_rectify undistort_rectify.cpp)
target_link_libraries(undistort_rectify ${OPENCV_LIBRARIES} "-lpopt")