﻿# CMakeList.txt : CMake project for OctoChip, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)

project(OctoChip)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

set(IS_DEBUG_BUILD CMAKE_BUILD_TYPE STREQUAL "Debug")

if (${IS_DEBUG_BUILD})
	add_compile_definitions(__DEBUG__)
endif()

add_definitions(-DDIRECTORY_PATH=\"${CMAKE_CURRENT_SOURCE_DIR}\")

set(SDL2_DIR "libs")

find_package(SDL2 REQUIRED)
include_directories(${SDL2_INCLUDE_DIR})

add_executable(OctoChip "src/octo_chip.cpp" "src/cpu.cpp"
	"src/keyboard.cpp" "src/audio.cpp" "src/renderer.cpp")
target_link_libraries(OctoChip ${SDL2_LIBRARIES})
