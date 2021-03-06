# Copyright (c) 2013-2016 Trillek contributors. See AUTHORS.txt for details
# Licensed under the terms of the LGPLv3. See licenses/lgpl-3.0.txt
cmake_minimum_required(VERSION 3.1)
project(trillek)

option(BUILD_CLIENT "Build the client" ON)
option(BUILD_SERVER "Build the server" ON)

# TEMPRARY WORKAROUND - Figure out a better solution (TODO)
#	asio does not include a CMake module so we have no easy way to locate it.
#	As a workaround, include the MacPorts and Fink 'includes' directories.
if (APPLE)
	include_directories("/opt/local/include")
	include_directories("/sw/include")
endif (APPLE)

# TODO: Perhaps add -pedantic -Wall -Wextra -Werror?
list(APPEND CMAKE_MODULE_PATH ${trillek_SOURCE_DIR}/deps)
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
include_directories(${trillek_SOURCE_DIR}/common)

if (MSVC)
	add_definitions(-DPROTOBUF_USE_DLLS)
endif ()

add_subdirectory(common)
if (BUILD_CLIENT)
	add_subdirectory(client)
endif ()
if (BUILD_SERVER)
	add_subdirectory(server)
endif ()
