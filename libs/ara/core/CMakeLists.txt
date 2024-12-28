cmake_minimum_required(VERSION 3.14)

project(ara_core)

add_library(
  ara_core 
  ${CMAKE_SOURCE_DIR}/libs/ara/core/optional.h
  ${CMAKE_SOURCE_DIR}/libs/ara/core/result.h
  ${CMAKE_SOURCE_DIR}/libs/ara/core/error_domain.h
  ${CMAKE_SOURCE_DIR}/libs/ara/core/error_code.h
  ${CMAKE_SOURCE_DIR}/libs/ara/core/error_code.cpp
  ${CMAKE_SOURCE_DIR}/libs/ara/core/instance_specifier.h
  ${CMAKE_SOURCE_DIR}/libs/ara/core/instance_specifier.cpp
)
