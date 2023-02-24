cmake_minimum_required(VERSION 3.10)
project(Rasterizer)

find_package(OpenCV REQUIRED
            PATHS ../opencv/opencv/build
            NO_DEFAULT_PATH)

set(CMAKE_CXX_STANDARD 17)

include_directories(../Eigen3/include)

add_executable(Rasterizer main.cpp rasterizer.hpp rasterizer.cpp Triangle.hpp Triangle.cpp)
target_link_libraries(Rasterizer ${OpenCV_LIBRARIES})

get_target_property(__dll_dbg opencv_world IMPORTED_LOCATION_DEBUG)
get_target_property(__dll_release opencv_world  IMPORTED_LOCATION_RELEASE)

add_custom_command(TARGET Rasterizer POST_BUILD        
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
    "$<$<CONFIG:debug>:${__dll_dbg}>$<$<CONFIG:release>:${__dll_release}>"
    $<TARGET_FILE_DIR:Rasterizer>)