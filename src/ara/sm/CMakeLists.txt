cmake_minimum_required(VERSION 3.14)

project(ara_sm)

add_library(
  ara_sm 
  ${CMAKE_SOURCE_DIR}/src/ara/sm/states.h
  ${CMAKE_SOURCE_DIR}/src/ara/sm/trigger.h
  ${CMAKE_SOURCE_DIR}/src/ara/sm/notifier.h
  ${CMAKE_SOURCE_DIR}/src/ara/sm/trigger_in.h
  ${CMAKE_SOURCE_DIR}/src/ara/sm/trigger_out.h
  ${CMAKE_SOURCE_DIR}/src/ara/sm/trigger_inout.h
)
