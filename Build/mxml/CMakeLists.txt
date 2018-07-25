cmake_minimum_required(VERSION 3.0.0 FATAL_ERROR)



set(CPP_DIR .)
set(HEADER_DIR .)


#The main options of project
PROJECT(mxml)

# Define Debug by default.
if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE "Debug")
  message(STATUS "Build type not specified: Use Debug by default.")
endif(NOT CMAKE_BUILD_TYPE)
# -D_USRDLL 

# Definition of Macros
add_definitions(
   -D_DEBUG 
   -DSTATIC_LIBRARY
   -DMXML1_EXPORTS 
)
if(MSVC)
    add_definitions(-D_CRT_SECURE_NO_WARNINGS)
endif()

# Defines outputs , depending Debug or Release.
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${MXML_BUILD_DIR}/lib")
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${MXML_BUILD_DIR}/lib")
set(CMAKE_EXECUTABLE_OUTPUT_DIRECTORY "${MXML_BUILD_DIR}/bin")


if(MSVC)
   set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} /W1 /MTd /Od /Zi /EHsc")
   set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /W1 /MTd /EHsc")
endif(MSVC)
if(NOT MSVC)
   set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
   if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
       set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libc++")
   endif()
endif(NOT MSVC)

#Add files to project
file(GLOB SRC_FILES
    ${CPP_DIR}/mmd.c
	${CPP_DIR}/mxml-attr.c
	${CPP_DIR}/mxml-entity.c
	${CPP_DIR}/mxml-file.c
	${CPP_DIR}/mxml-get.c
	${CPP_DIR}/mxml-index.c
	${CPP_DIR}/mxml-node.c
	${CPP_DIR}/mxml-private.c
	${CPP_DIR}/mxml-search.c
	${CPP_DIR}/mxml-set.c
	${CPP_DIR}/mxml-string.c
    ${HEADER_DIR}/config.h
	${HEADER_DIR}/mmd.h
	${HEADER_DIR}/mxml.h
	${HEADER_DIR}/mxml-private.h
)

# Add library to build.
add_library(mxml STATIC
   ${SRC_FILES}
)

SET_TARGET_PROPERTIES(mxml PROPERTIES LINKER_LANGUAGE C)

if ( MSVC )
    set_target_properties( mxml PROPERTIES ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_ARCHIVE_OUTPUT_DIRECTORY} )
    set_target_properties( mxml PROPERTIES ARCHIVE_OUTPUT_DIRECTORY_DEBUG ${CMAKE_ARCHIVE_OUTPUT_DIRECTORY} )
    set_target_properties( mxml PROPERTIES ARCHIVE_OUTPUT_DIRECTORY_RELEASE ${CMAKE_ARCHIVE_OUTPUT_DIRECTORY} )
    # etc for the other available configuration types (MinSizeRel, RelWithDebInfo)
endif ( MSVC )
