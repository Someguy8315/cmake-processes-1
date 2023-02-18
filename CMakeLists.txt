cmake_minimum_required(VERSION 3.15)

project(main)

add_executable(main main.c)

# find the Python 3 interpreter
find_package(Python3 REQUIRED)

# execute the python script when the main target is built
add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
    COMMAND ${Python3_EXECUTABLE} ${CMAKE_SOURCE_DIR}/scripts/test.py
)
