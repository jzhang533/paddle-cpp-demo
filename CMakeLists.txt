cmake_minimum_required(VERSION 3.10)
project(paddle_cpp_demo CXX)
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(PythonLibs REQUIRED)
find_package(pybind11 CONFIG REQUIRED)

message(STATUS "PADDLE_LIBRARY = ${PADDLE_LIBRARY}")

include_directories(${PYTHON_INCLUDE_DIRS})
include_directories(${PADDLE_LIBRARY}/include)

set(link_libraries ${PADDLE_LIBRARY}/fluid/libpaddle.so)

set(link_libraries_path ${CMAKE_SOURCE_DIR};${PADDLE_LIBRARY}/libs;${PADDLE_LIBRARY}/fluid/)

include_directories(${include_dirs})
link_directories(${link_libraries_path})

set(name main)
set(source main.cc)
add_executable(${name} ${source})
target_link_libraries(${name} ${link_libraries} ${PYTHON_LIBRARIES} pybind11::embed)
