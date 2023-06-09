cmake_minimum_required(VERSION 3.22.1)

project(wrapper)

include_directories("${CMAKE_CURRENT_SOURCE_DIR}/src/main/cpp/include")
add_library(realsense2 SHARED IMPORTED)
set_target_properties(
        realsense2
        PROPERTIES
        IMPORTED_LOCATION
        ${CMAKE_CURRENT_SOURCE_DIR}/build/jni/${ANDROID_ABI}/librealsense2.so
)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)

# Add sources
add_library(${PROJECT_NAME} SHARED
        src/main/cpp/wrapper.hpp
        src/main/cpp/wrapper.cpp
        )

# Required for librealsense2 for some reason
find_library(log-lib log)

# Link to librealsense2
target_link_libraries(${PROJECT_NAME}
        ${log-lib}
        realsense2
        )