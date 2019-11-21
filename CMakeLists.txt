
cmake_minimum_required(VERSION 2.8.11 FATAL_ERROR)

#version variables, major and minor must be 1 character only
SET(LICENSECC_MAJOR_VERSION 1)
SET(LICENSECC_MINOR_VERSION 1)
SET(LICENSECC_PATCH_VERSION 0 CACHE STRING "License++ patch version string")
SET(LICENSECC_INT_VERSION "${LICENSECC_MAJOR_VERSION}${LICENSECC_MINOR_VERSION}${LICENSECC_PATCH_VERSION}")
SET(LICENSECC_VERSION "${LICENSECC_MAJOR_VERSION}.${LICENSECC_MINOR_VERSION}.${LICENSECC_PATCH_VERSION}")
SET(LICENSECC_SHORT_LICENSE "BSD Software License")

SET(CMAKE_DISABLE_SOURCE_CHANGES ON)
SET(CMAKE_DISABLE_IN_SOURCE_BUILD ON)
SET(CMAKE_VERBOSE_MAKEFILE ON CACHE BOOL "CMake verbose")

project (license++ C CXX )
SET(RELEASE_BUILD 1)
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pipe -fmessage-length=0 -std=c++11 -Wuninitialized -fPIC") #-Wall
SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -pipe -fmessage-length=0 -Wall -Wuninitialized -fPIC")
SET(CMAKE_EXE_LINKER_FLAGS  "-pthread -static-libstdc++")
SET(CMAKE_EXE_LINKER_FLAGS_RELEASE "-Wl,--strip-all -static-libstdc++") #-static

include_directories(${OPENSSL_INCLUDE_DIR})
list(APPEND EXTERNAL_LIBS ${OPENSSL_CRYPTO_LIBRARY})
MESSAGE(STATUS "Found openssl version ${OPENSSL_VERSION} ")
list(APPEND EXTERNAL_LIBS ${ZLIB_LIBRARIES})
MESSAGE(STATUS "Found zlib version ${ZLIB_VERSION} ")
list(APPEND EXTERNAL_LIBS "-ldl")
SET(HAVE_64BIT_SIZE_T 1)

configure_file (
    "src/build_properties.h.in"
    "${CMAKE_CURRENT_BINARY_DIR}/build_properties.h"
    )

message( STATUS "C compiler        : " ${CMAKE_C_COMPILER})
message( STATUS "C compiler flags  : " ${CMAKE_C_FLAGS})
message( STATUS "CXX compiler      : " ${CMAKE_CXX_COMPILER})
message( STATUS "CXX compiler flags: " ${CMAKE_CXX_FLAGS})
message( STATUS "CXX compiler flags debug : " ${CMAKE_CXX_FLAGS_DEBUG})
message( STATUS "CXX compiler flags release: " ${CMAKE_CXX_FLAGS_RELEASE})
if(CMAKE_BUILD_TYPE)
    message( STATUS "Build type        : " ${CMAKE_BUILD_TYPE})
endif(CMAKE_BUILD_TYPE)
message( STATUS "Install prefix    : " ${CMAKE_INSTALL_PREFIX})

#include build directory to find build_properties.h and pri/pub keys
include_directories(${CMAKE_SOURCE_DIR} ${CMAKE_CURRENT_BINARY_DIR})

add_subdirectory(src)
