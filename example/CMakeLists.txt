cmake_minimum_required(VERSION 2.8.11)

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

add_executable(example example.cpp)

target_link_libraries(example licensecc_static)
