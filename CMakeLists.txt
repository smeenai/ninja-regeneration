cmake_minimum_required(VERSION 3.13.4)
project(ninja-regeneration C)

add_executable(generator generator.c)
add_custom_command(
  OUTPUT generated.cmake
  COMMAND $<TARGET_FILE:generator> > generated.cmake
  DEPENDS generator)
add_custom_target(generate DEPENDS generated.cmake)
execute_process(
  COMMAND ${CMAKE_COMMAND} -E touch ${CMAKE_CURRENT_BINARY_DIR}/generated.cmake)
include(${CMAKE_CURRENT_BINARY_DIR}/generated.cmake)
