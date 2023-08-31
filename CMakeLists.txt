cmake_minimum_required(VERSION 3.16)
project(minheap)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_BUILD_TYPE Debug)

# set(ALL_SRC "")

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

add_executable(main main.cc)