cmake_minimum_required(VERSION 3.14)

project(ara_log)

add_library(
  ara_log
  ${CMAKE_SOURCE_DIR}/libs/ara/log/argument.h
  ${CMAKE_SOURCE_DIR}/libs/ara/log/log_stream.h
  ${CMAKE_SOURCE_DIR}/libs/ara/log/log_stream.cpp
  ${CMAKE_SOURCE_DIR}/libs/ara/log/logger.h
  ${CMAKE_SOURCE_DIR}/libs/ara/log/logger.cpp
  ${CMAKE_SOURCE_DIR}/libs/ara/log/logging_framework.h
  ${CMAKE_SOURCE_DIR}/libs/ara/log/logging_framework.cpp
  ${CMAKE_SOURCE_DIR}/libs/ara/log/sink/console_log_sink.h
  ${CMAKE_SOURCE_DIR}/libs/ara/log/sink/console_log_sink.cpp
  ${CMAKE_SOURCE_DIR}/libs/ara/log/sink/file_log_sink.h
  ${CMAKE_SOURCE_DIR}/libs/ara/log/sink/file_log_sink.cpp
  ${CMAKE_SOURCE_DIR}/libs/ara/log/sink/log_sink.h
  ${CMAKE_SOURCE_DIR}/libs/ara/log/sink/log_sink.cpp
)
