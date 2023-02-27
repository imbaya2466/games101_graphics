cmake_minimum_required (VERSION 2.8.11)
project (graphics)

find_package(OpenCV REQUIRED
            PATHS ./opencv/opencv/build
            NO_DEFAULT_PATH)

add_subdirectory(mission0)
add_subdirectory(mission1)
add_subdirectory(mission2)
add_subdirectory(mission3)