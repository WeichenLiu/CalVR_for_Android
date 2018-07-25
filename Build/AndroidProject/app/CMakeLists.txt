# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.



cmake_minimum_required(VERSION 3.4.1)

# for more detailed linker message
SET( GCC_COVERAGE_LINK_FLAGS    "-v") 
SET( CMAKE_EXE_LINKER_FLAGS  "${CMAKE_EXE_LINKER_FLAGS} ${GCC_COVERAGE_LINK_FLAGS}" )
SET( CMAKE_SHARED_LINKER_FLAGS  "${CMAKE_SHARED_LINKER_FLAGS} ${GCC_COVERAGE_LINK_FLAGS}" )
SET( CMAKE_STATIC_LINKER_FLAGS  "${CMAKE_STATIC_LINKER_FLAGS} ${GCC_COVERAGE_LINK_FLAGS}" )


# set variable for osg					   
include(CMakeLists-osg.txt)
# set variable for mxml	
include(CMakeLists-mxml.txt)
# set variable for calvr
include(CMakeLists-calvr.txt)

include(CMakeLists-prebuild.txt)
#include(CMakeLists-jni.txt)
