########################################################################
# Requirements and dependencies:
########################################################################

cmake_minimum_required(VERSION 3.14)
project(Adaptive_Platform)

# This AUTOSAR Adaptive Platform requires C++14
set(CMAKE_CXX_STANDARD 14)

# Enable 'rdyamic' switch to export the executable's symbols for debugging
set(CMAKE_ENABLE_EXPORTS ON)

include(FetchContent)

########################################################################
# Fetching dependencies
########################################################################

FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/58d77fa8070e8cec2dc1ed015d66b454c8d78850.zip
)

FetchContent_Declare(
  libcurl
  URL https://github.com/curl/curl/archive/3027611ca6d4cc5510d2d0fccc3e5a074e09a2fb.zip
)

FetchContent_Declare(
  jsoncpp_lib
  URL https://github.com/open-source-parsers/jsoncpp/archive/5defb4ed1a4293b8e2bf641e16b156fb9de498cc.zip
)

FetchContent_Declare(
  Async-BSD-Socket-Lib
  URL https://github.com/langroodi/Async-BSD-Socket-Lib/archive/8c84da8f4b5e7552b41a54c92acb0b4565d07024.zip
)

FetchContent_Declare(
  OBD-II-Emulator
  URL https://github.com/langroodi/OBD-II-Emulator/archive/2c33042a6397d7030f3bafb57b6b88b913d95cb2.zip
)

FetchContent_Declare(
  Doip-Lib
  URL https://github.com/langroodi/Doip-Lib/archive/5acfd483eb3dc90429a98dbe4b70de8b1db68af6.zip
)

FetchContent_MakeAvailable(
  googletest
  libcurl
  jsoncpp_lib
  Async-BSD-Socket-Lib
  OBD-II-Emulator
  Doip-Lib
)

########################################################################
# Options:
########################################################################

option(build_tests "Build all the tests." ON)

########################################################################
# Subdirectory structure:
########################################################################

macro(add_if_exists dir)
  if(EXISTS ${CMAKE_SOURCE_DIR}/${dir})
    add_subdirectory(${dir})
  else()
    message(WARNING "Directory ${dir} does not exist.")
  endif()
endmacro()

# Check for required source files before adding subdirectories
macro(check_required_files)
  set(required_files
    "src/arxml/pugixml.hpp"
    "src/ara/core/result.h"
    "src/ara/core/error_domain.h"
    "src/ara/sm/trigger.h"
    "src/ara/phm/checkpoint_communicator.cpp"
  )
  foreach(file ${required_files})
    if(NOT EXISTS ${CMAKE_SOURCE_DIR}/${file})
      message(FATAL_ERROR "Required file ${file} does not exist.")
    endif()
  endforeach()
endmacro()

check_required_files()

add_if_exists(src/arxml)
add_if_exists(src/ara/core)
add_if_exists(src/ara/log)
add_if_exists(src/ara/com)
add_if_exists(src/ara/sm)
add_if_exists(src/ara/exec)
add_if_exists(src/ara/diag)
add_if_exists(src/ara/phm)
# add_if_exists(src/application)  # Add this line to include the application directory

# Ensure required source files are added in their respective CMakeLists.txt
set_target_properties(ara_sm PROPERTIES LINKER_LANGUAGE CXX)

########################################################################
# Installation rules:
########################################################################

# Define installation directories
set(CMAKE_INSTALL_PREFIX /usr/local/ara_libs)

# Install the library and headers for each component
install(DIRECTORY src/arxml/
        DESTINATION include/arxml
        FILES_MATCHING PATTERN "*.h")

install(DIRECTORY src/ara/core/
        DESTINATION include/ara/core
        FILES_MATCHING PATTERN "*.h")

install(DIRECTORY src/ara/log/
        DESTINATION include/ara/log
        FILES_MATCHING PATTERN "*.h")

install(DIRECTORY src/ara/com/
        DESTINATION include/ara/com
        FILES_MATCHING PATTERN "*.h")

install(DIRECTORY src/ara/sm/
        DESTINATION include/ara/sm
        FILES_MATCHING PATTERN "*.h")

install(DIRECTORY src/ara/exec/
        DESTINATION include/ara/exec
        FILES_MATCHING PATTERN "*.h")

install(DIRECTORY src/ara/diag/
        DESTINATION include/ara/diag
        FILES_MATCHING PATTERN "*.h")

install(DIRECTORY src/ara/phm/
        DESTINATION include/ara/phm
        FILES_MATCHING PATTERN "*.h")

install(DIRECTORY src/async_bsd_socket_lib/
        DESTINATION include/async_bsd_socket_lib
        FILES_MATCHING PATTERN "*.h")

# Install the built libraries
install(TARGETS arxml ara_core ara_log ara_com ara_sm ara_exec ara_diag ara_phm async_bsd_socket_lib
        ARCHIVE DESTINATION lib
        LIBRARY DESTINATION lib
        RUNTIME DESTINATION bin)


