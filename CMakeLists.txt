PROJECT(moost)

CMAKE_MINIMUM_REQUIRED(VERSION 2.4)

SET(CMAKE_VERBOSE_MAKEFILE ON)

# binaries get installed here
SET(CMAKE_INSTALL_PREFIX "/usr/")

#add definitions, compiler switches, etc.
ADD_DEFINITIONS(-Wall -O2 -DNDEBUG -g `getconf LFS_CFLAGS`)

INCLUDE_DIRECTORIES(include
                    /opt/local/include
                    )

IF(CMAKE_SYSTEM_NAME STREQUAL "Linux" AND CMAKE_COMPILER_IS_GNUCC)
  ADD_LIBRARY(boost_coroutine STATIC
              libs/coroutine/src/coroutine.cpp
              libs/coroutine/src/swapcontext.cpp
             )
ELSE(CMAKE_SYSTEM_NAME STREQUAL "Linux" AND CMAKE_COMPILER_IS_GNUCC)
  ADD_LIBRARY(boost_coroutine STATIC
              libs/coroutine/src/coroutine.cpp
             )
ENDIF(CMAKE_SYSTEM_NAME STREQUAL "Linux" AND CMAKE_COMPILER_IS_GNUCC)
            
INSTALL(TARGETS boost_coroutine ARCHIVE DESTINATION lib)

INSTALL(DIRECTORY boost/coroutine DESTINATION include/boost PATTERN ".svn" EXCLUDE)
