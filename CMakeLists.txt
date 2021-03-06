cmake_minimum_required(VERSION 2.6)

project(neb)

set(PROJECT_VERSION "0.0")
set(PROJECT_CONTACT "ruehle@vota.org")

# if not specified by user, the standard build type is release
if(NOT CMAKE_BUILD_TYPE)
  #Release comes with -O3 by default
  set(CMAKE_BUILD_TYPE Release CACHE STRING "Choose the type of build, options are: None Debug Release RelWithDebInfo MinSizeRel." FORCE)
endif(NOT CMAKE_BUILD_TYPE)

enable_language(CXX)
ADD_DEFINITIONS(-Wall)

include(CheckCXXCompilerFlag)
CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)
CHECK_CXX_COMPILER_FLAG("-std=c++0x" COMPILER_SUPPORTS_CXX0X)
if(COMPILER_SUPPORTS_CXX11)
  ADD_DEFINITIONS(-std=c++11)
elseif(COMPILER_SUPPORTS_CXX0X)
  ADD_DEFINITIONS(-std=c++0x)
else()
        message(STATUS "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support. Please use a different C++ compiler.")
endif()
add_subdirectory(src)
add_subdirectory(tests)
add_subdirectory(examples)


