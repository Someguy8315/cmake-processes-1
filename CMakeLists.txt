cmake_minimum_required(VERSION 3.15)

project(main)

add_executable(main main.c)

# find the Python 3 interpreter
find_package(Python3 REQUIRED)

# create a custom target that depends on a non-existent file
add_custom_target(
    custom_target ALL # the ALL parameter ensures that this target will always be built
    DEPENDS ${CMAKE_CURRENT_BINARY_DIR}/__header.h
)

# always execute the python script

# output option
add_custom_command(
    OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/__header.h
    COMMAND ${Python3_EXECUTABLE} ${CMAKE_SOURCE_DIR}/scripts/test.py
)

# target option (can specify when to trigger: before build/link and after build)
add_custom_command(
    TARGET custom_target PRE_BUILD
    COMMAND ${Python3_EXECUTABLE} ${CMAKE_SOURCE_DIR}/scripts/test.py
)
