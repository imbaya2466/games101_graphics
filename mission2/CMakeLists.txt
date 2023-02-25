cmake_minimum_required(VERSION 3.10)
project(Rasterizer2)

set(CMAKE_CXX_STANDARD 17)

include_directories(../Eigen3/include)

add_executable(Rasterizer2 main.cpp rasterizer.hpp rasterizer.cpp global.hpp Triangle.hpp Triangle.cpp)
target_link_libraries(Rasterizer2 ${OpenCV_LIBRARIES})

get_target_property(__dll_dbg opencv_world IMPORTED_LOCATION_DEBUG)
get_target_property(__dll_release opencv_world  IMPORTED_LOCATION_RELEASE)

add_custom_command(TARGET Rasterizer2 POST_BUILD        
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
    "$<$<CONFIG:debug>:${__dll_dbg}>$<$<CONFIG:release>:${__dll_release}>"
    $<TARGET_FILE_DIR:Rasterizer2>)