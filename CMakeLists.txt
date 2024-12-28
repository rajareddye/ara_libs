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
  DOWNLOAD_EXTRACT_TIMESTAMP TRUE
)

FetchContent_Declare(
  libcurl
  URL https://github.com/curl/curl/archive/3027611ca6d4cc5510d2d0fccc3e5a074e09a2fb.zip
  DOWNLOAD_EXTRACT_TIMESTAMP TRUE
)

FetchContent_Declare(
  jsoncpp_lib
  URL https://github.com/open-source-parsers/jsoncpp/archive/5defb4ed1a4293b8e2bf641e16b156fb9de498cc.zip
  DOWNLOAD_EXTRACT_TIMESTAMP TRUE
)

FetchContent_Declare(
  Async-BSD-Socket-Lib
  URL https://github.com/langroodi/Async-BSD-Socket-Lib/archive/8c84da8f4b5e7552b41a54c92acb0b4565d07024.zip
  DOWNLOAD_EXTRACT_TIMESTAMP TRUE
)

FetchContent_Declare(
  OBD-II-Emulator
  URL https://github.com/langroodi/OBD-II-Emulator/archive/2c33042a6397d7030f3bafb57b6b88b913d95cb2.zip
  DOWNLOAD_EXTRACT_TIMESTAMP TRUE
)

FetchContent_Declare(
  Doip-Lib
  URL https://github.com/langroodi/Doip-Lib/archive/5acfd483eb3dc90429a98dbe4b70de8b1db68af6.zip
  DOWNLOAD_EXTRACT_TIMESTAMP TRUE
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
# Include Directories
########################################################################

include_directories(
  build/_deps/googletest-src/include
  build/_deps/libcurl-src/include
  build/_deps/jsoncpp_lib-src/include
  build/_deps/async-bsd-socket-lib-src/include
  build/_deps/obd-ii-emulator-src/include
  build/_deps/doip-lib-src/include
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
    "libs/arxml/pugixml.hpp"
    "libs/ara/core/result.h"
    "libs/ara/core/error_domain.h"
    "libs/ara/sm/trigger.h"
    "libs/ara/phm/checkpoint_communicator.cpp"
  )
  foreach(file ${required_files})
    if(NOT EXISTS ${CMAKE_SOURCE_DIR}/${file})
      message(FATAL_ERROR "Required file ${file} does not exist.")
    endif()
  endforeach()
endmacro()

check_required_files()

add_if_exists(libs/arxml)
add_if_exists(libs/ara/core)
add_if_exists(libs/ara/log)
add_if_exists(libs/ara/com)
add_if_exists(libs/ara/sm)
add_if_exists(libs/ara/exec)
add_if_exists(libs/ara/diag)
add_if_exists(libs/ara/phm)

# Ensure required source files are added in their respective CMakeLists.txt
set_target_properties(ara_sm PROPERTIES LINKER_LANGUAGE CXX)

########################################################################
# Installation rules:
########################################################################

# Define installation directories
set(CMAKE_INSTALL_PREFIX /usr/local/ara_libs)

# Install the library and headers for each component
install(DIRECTORY libs/arxml/
        DESTINATION include/arxml
        FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp")

install(DIRECTORY libs/ara/core/
        DESTINATION include/ara/core
        FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp")

install(DIRECTORY libs/ara/log/
        DESTINATION include/ara/log
        FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp")

install(DIRECTORY libs/ara/com/
        DESTINATION include/ara/com
        FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp")

install(DIRECTORY libs/ara/sm/
        DESTINATION include/ara/sm
        FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp")

install(DIRECTORY libs/ara/exec/
        DESTINATION include/ara/exec
        FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp")

install(DIRECTORY libs/ara/diag/
        DESTINATION include/ara/diag
        FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp")

install(DIRECTORY libs/ara/phm/
        DESTINATION include/ara/phm
        FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp")

install(DIRECTORY build/_deps/async-bsd-socket-lib-src/include/asyncbsdsocket/
        DESTINATION include/asyncbsdsocket
        FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp")

install(DIRECTORY build/_deps/googletest-src/include/
        DESTINATION include/googletest
        FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp")

install(DIRECTORY build/_deps/jsoncpp_lib-src/include/
        DESTINATION include/jsoncpp
        FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp")

install(DIRECTORY build/_deps/libcurl-src/include/
        DESTINATION include
        FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp")

install(DIRECTORY build/_deps/obd-ii-emulator-src/include/
        DESTINATION include/
        FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp")

install(DIRECTORY build/_deps/doip-lib-src/include/
        DESTINATION include
        FILES_MATCHING PATTERN "*.h" PATTERN "*.hpp")

# Ensure all .cpp files in libs/ara/core are installed
install(FILES
        libs/ara/core/error_code.cpp
        libs/ara/core/instance_specifier.cpp
        DESTINATION lib/ara/core
)

install(TARGETS arxml ara_core ara_log ara_com ara_sm ara_exec ara_diag ara_phm async_bsd_socket_lib
        ARCHIVE DESTINATION lib
        LIBRARY DESTINATION lib
        RUNTIME DESTINATION bin)

# Install the built libraries, wrapped with `if(TARGET ...)` for robustness
if(TARGET jsoncpp)
  install(TARGETS jsoncpp
          EXPORT jsoncppTargets
          RUNTIME DESTINATION bin
          LIBRARY DESTINATION lib
          ARCHIVE DESTINATION lib)
endif()

if(TARGET async_bsd_socket_lib)
  install(TARGETS async_bsd_socket_lib
          EXPORT asyncBsdSocketTargets
          RUNTIME DESTINATION bin
          LIBRARY DESTINATION lib
          ARCHIVE DESTINATION lib)
endif()

if(TARGET obd_ii_emulator)
  install(TARGETS obd_ii_emulator
          EXPORT obdIiEmulatorTargets
          RUNTIME DESTINATION bin
          LIBRARY DESTINATION lib
          ARCHIVE DESTINATION lib)
endif()

if(TARGET doip_lib)
  install(TARGETS doip_lib
          EXPORT doipLibTargets
          RUNTIME DESTINATION bin
          LIBRARY DESTINATION lib
          ARCHIVE DESTINATION lib)
endif()

if(TARGET gtest AND TARGET gtest_main)
  install(TARGETS gtest gtest_main
          EXPORT googletestTargets
          RUNTIME DESTINATION bin
          LIBRARY DESTINATION lib
          ARCHIVE DESTINATION lib)
endif()

if(TARGET curl)
  install(TARGETS curl
          EXPORT libcurlTargets
          RUNTIME DESTINATION bin
          LIBRARY DESTINATION lib
          ARCHIVE DESTINATION lib)
endif()

########################################################################
# Uninstallation rules:
########################################################################

# Add an uninstall target
if(NOT TARGET uninstall)
    configure_file(
        "${CMAKE_CURRENT_SOURCE_DIR}/cmake_uninstall.cmake.in"
        "${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake"
        @ONLY
    )

    add_custom_target(uninstall
        COMMAND ${CMAKE_COMMAND} -P ${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake
    )
endif()

########################################################################
# End of file
########################################################################
