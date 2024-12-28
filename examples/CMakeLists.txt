cmake_minimum_required(VERSION 3.14)
project(AppExample)

# Set C++ standard
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Include paths
include_directories(
    ${CMAKE_SOURCE_DIR}
    /usr/local/ara_libs/include
)

# Add library path explicitly
link_directories(/usr/local/ara_libs/lib)

add_executable(
  MyApplication
  main.cpp
  ./application/extended_vehicle.h 
  ./application/extended_vehicle.cpp
  ./application/helper/argument_configuration.h  
  ./application/helper/argument_configuration.cpp
  ./application/helper/curl_wrapper.h
  ./application/helper/curl_wrapper.cpp
  ./application/helper/network_configuration.h
  ./application/helper/network_configuration.cpp
  ./application/helper/rpc_configuration.h
  ./application/helper/rpc_configuration.cpp
  ./application/helper/read_data_by_identifier.h
  ./application/helper/read_data_by_identifier.cpp
  ./application/helper/memory_cache.h
  ./application/helper/log_recovery_action.h
  ./application/helper/log_recovery_action.cpp
  ./application/helper/fifo_checkpoint_communicator.h
  ./application/helper/fifo_checkpoint_communicator.cpp
  ./application/doip/vehicle_id_request_handler.h 
  ./application/doip/vehicle_id_request_handler.cpp
  ./application/doip/diag_message_handler.h
  ./application/doip/diag_message_handler.cpp
  ./application/doip/doip_server.h
  ./application/doip/doip_server.cpp
  ./application/doip/doip_client.h
  ./application/doip/doip_client.cpp
  ./application/doip/obd_to_doip_converter.h
  ./application/doip/obd_to_doip_converter.cpp
  ./application/platform/state_management.h
  ./application/platform/state_management.cpp
  ./application/platform/execution_management.h
  ./application/platform/execution_management.cpp
  ./application/platform/diagnostic_manager.h
  ./application/platform/diagnostic_manager.cpp
  ./application/platform/platform_health_management.h
  ./application/platform/platform_health_management.cpp

)

# Link required libraries
target_link_libraries(MyApplication
    arxml
    ara_core
    ara_log
    ara_com
    ara_sm
    ara_exec
    ara_diag
    ara_phm
    async_bsd_socket_lib
    jsoncpp
    curl
    gmock
    gtest
    doip_lib
    obd_ii_emulator

)

