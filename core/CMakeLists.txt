message(STATUS "adding submodule kernel")

cmake_minimum_required(VERSION 3.7.2)
set(CMAKE_C_STANDARD 11)

execute_process(COMMAND uname -r OUTPUT_VARIABLE v OUTPUT_STRIP_TRAILING_WHITESPACE)
set(path /lib/modules/${v}/build/include/)
message(STATUS ${path})
include_directories(${path})

add_subdirectory(filter)
add_subdirectory(logging)
add_subdirectory(messaging)

add_definitions(-DCONFIG_NETFILTER)
add_executable(TEST_HEADER test_module.c)