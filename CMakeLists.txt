# Copyright (C) 2010 RobotCub Consortium
# Author: Jorhabib Eljaik, Marco Randazzo
# CopyPolicy: Released under the terms of the GNU GPL v2.0.

cmake_minimum_required(VERSION 2.8.7)
SET(PROJECTNAME comStepper)
PROJECT(${PROJECTNAME})

SET(folder_source ./src/main.cpp ./src/comStepper.cpp ./src/rangeCheck.cpp ./src/util.cpp)
SET(folder_header ./src/comStepper.h ./src/rangeCheck.h ./src/util.h)

SOURCE_GROUP("Source Files" FILES ${folder_source})
SOURCE_GROUP("Header Files" FILES ${folder_header})

FIND_PACKAGE(YARP REQUIRED)
FIND_PACKAGE(ICUB REQUIRED)

set(YCM_USE_CMAKE_PROPOSED TRUE CACHE BOOL "Use files including unmerged cmake patches")

find_package(YCM REQUIRED)

# add yarp definitions
add_definitions(${YARP_DEFINES})   #this contains also -D_REENTRANT

# pick up yarp's cmake scripts
list(APPEND CMAKE_MODULE_PATH ${YARP_MODULE_PATH})
include(YarpInstallationHelpers)

# add yarp include directories
INCLUDE_DIRECTORIES(${iDyn_INCLUDE_DIRS}
                    ${ICUB_INCLUDE_DIRS}
                    ${YARP_INCLUDE_DIRS})
                    
ADD_EXECUTABLE(${PROJECTNAME} ${folder_source} ${folder_header})

TARGET_LINK_LIBRARIES(${PROJECTNAME} iDyn ${YARP_LIBRARIES})

INSTALL(TARGETS ${PROJECTNAME} DESTINATION bin)

add_subdirectory(app)

include(AddUninstallTarget)
