cmake_minimum_required(VERSION 3.14)

project(ara_exec)

# Add include directories for Async-BSD-Socket-Lib
include_directories(${async-bsd-socket-lib_SOURCE_DIR}/include)

add_library(
  ara_exec
  ${CMAKE_SOURCE_DIR}/src/ara/exec/worker_thread.h
  ${CMAKE_SOURCE_DIR}/src/ara/exec/worker_thread.cpp
  ${CMAKE_SOURCE_DIR}/src/ara/exec/worker_runnable.h
  ${CMAKE_SOURCE_DIR}/src/ara/exec/deterministic_client.h
  ${CMAKE_SOURCE_DIR}/src/ara/exec/deterministic_client.cpp
  ${CMAKE_SOURCE_DIR}/src/ara/exec/execution_client.h
  ${CMAKE_SOURCE_DIR}/src/ara/exec/execution_client.cpp
  ${CMAKE_SOURCE_DIR}/src/ara/exec/execution_server.h
  ${CMAKE_SOURCE_DIR}/src/ara/exec/execution_server.cpp
  ${CMAKE_SOURCE_DIR}/src/ara/exec/function_group.h
  ${CMAKE_SOURCE_DIR}/src/ara/exec/function_group.cpp
  ${CMAKE_SOURCE_DIR}/src/ara/exec/function_group_state.h
  ${CMAKE_SOURCE_DIR}/src/ara/exec/function_group_state.cpp
  ${CMAKE_SOURCE_DIR}/src/ara/exec/exec_error_domain.h
  ${CMAKE_SOURCE_DIR}/src/ara/exec/exec_error_domain.cpp
  ${CMAKE_SOURCE_DIR}/src/ara/exec/exec_exception.h
  ${CMAKE_SOURCE_DIR}/src/ara/exec/exec_exception.cpp
  ${CMAKE_SOURCE_DIR}/src/ara/exec/execution_error_event.h
  ${CMAKE_SOURCE_DIR}/src/ara/exec/state_client.h
  ${CMAKE_SOURCE_DIR}/src/ara/exec/state_client.cpp
  ${CMAKE_SOURCE_DIR}/src/ara/exec/state_server.h
  ${CMAKE_SOURCE_DIR}/src/ara/exec/state_server.cpp
  ${CMAKE_SOURCE_DIR}/src/ara/exec/helper/atomic_optional.h
  ${CMAKE_SOURCE_DIR}/src/ara/exec/helper/modelled_process.h
  ${CMAKE_SOURCE_DIR}/src/ara/exec/helper/modelled_process.cpp
)


