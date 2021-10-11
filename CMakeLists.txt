#
# @author zouxiaoliang
# @date 2021/10/11
#

cmake_minimum_required(VERSION 3.19)
project(thirdparty_libnjson LANGUAGES C CXX)

message(STATUS "toolchain: ${CMAKE_SYSROOT}")
message(STATUS "cpu arch: ${CMAKE_SYSTEM_PROCESSOR}")

function(libnjsonMain)
    set(library_root "${CMAKE_CURRENT_SOURCE_DIR}/json")
    message(STATUS "njson root path: ${library_root}")

    add_library(thirdparty_libnjson INTERFACE)
    target_include_directories(thirdparty_libnjson SYSTEM INTERFACE
      "${library_root}/single_include"
    )
endfunction()

libnjsonMain()

