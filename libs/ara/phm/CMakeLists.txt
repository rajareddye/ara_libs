cmake_minimum_required(VERSION 3.14)

project(ara_phm)

add_library(
  ara_phm 
  ${CMAKE_SOURCE_DIR}/libs/ara/phm/checkpoint_communicator.h
  ${CMAKE_SOURCE_DIR}/libs/ara/phm/checkpoint_communicator.cpp
  ${CMAKE_SOURCE_DIR}/libs/ara/phm/supervised_entity.h
  ${CMAKE_SOURCE_DIR}/libs/ara/phm/supervised_entity.cpp
  ${CMAKE_SOURCE_DIR}/libs/ara/phm/recovery_action.h
  ${CMAKE_SOURCE_DIR}/libs/ara/phm/recovery_action.cpp
  ${CMAKE_SOURCE_DIR}/libs/ara/phm/supervisors/elementary_supervision.h
  ${CMAKE_SOURCE_DIR}/libs/ara/phm/supervisors/elementary_supervision.cpp
  ${CMAKE_SOURCE_DIR}/libs/ara/phm/supervisors/alive_supervision.h
  ${CMAKE_SOURCE_DIR}/libs/ara/phm/supervisors/alive_supervision.cpp
  ${CMAKE_SOURCE_DIR}/libs/ara/phm/supervisors/deadline_supervision.h
  ${CMAKE_SOURCE_DIR}/libs/ara/phm/supervisors/deadline_supervision.cpp
  ${CMAKE_SOURCE_DIR}/libs/ara/phm/supervisors/global_supervision.h
  ${CMAKE_SOURCE_DIR}/libs/ara/phm/supervisors/global_supervision.cpp
)
