#
# @author zouxiaoliang
# @date 2021/10/11
#

cmake_minimum_required(VERSION 3.19)
project(libnjson-cmake LANGUAGES C CXX)

message(STATUS "toolchain: ${CMAKE_SYSROOT}")
message(STATUS "cpu arch: ${CMAKE_SYSTEM_PROCESSOR}")

set(HAS_THIRDPARTY_NJSON ON PARENT_SCOPE)

set(EXTERNAL_INSTALL_LOCATION ${CMAKE_CURRENT_BINARY_DIR}/external)

# function(libnjsonMain)
# set(library_root "${CMAKE_CURRENT_SOURCE_DIR}/json")
# message(STATUS "njson root path: ${library_root}")

# add_library(thirdparty_libnjson INTERFACE)
# target_include_directories(thirdparty_libnjson SYSTEM INTERFACE
# "${library_root}/single_include"
# )
# endfunction()

# libnjsonMain()
function(main)
  ExternalProject_Add(
    njson
    PREFIX ${EXTERNAL_INSTALL_LOCATION}

    # GIT_REPOSITORY https://github.com/nlohmann/json.git
    # GIT_TAG master
    URL https://github.com/nlohmann/json/archive/refs/tags/v3.11.3.tar.gz
    CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${EXTERNAL_INSTALL_LOCATION}
    UPDATE_DISCONNECTED TRUE
  )

  add_library(thirdparty_libnjson INTERFACE)
  add_dependencies(thirdparty_libnjson njson)
  target_include_directories(thirdparty_libnjson INTERFACE
    ${EXTERNAL_INSTALL_LOCATION}/include
  )
endfunction(main)

main()
