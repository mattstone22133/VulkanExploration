cmake_minimum_required(VERSION 3.15 FATAL_ERROR)

set(EXECUTABLE_NAME VulkanExploration)
project("${EXECUTABLE_NAME}")

set(CMAKE_CXX_STANDARD 17)
find_package(Vulkan REQUIRED)

set(SHARED_CMAKE_UTILITES_DIR "${CMAKE_CURRENT_LIST_DIR}/CMake" CACHE STRING "global location to include helpers from" FORCE) 

add_subdirectory("projects/vulkan-tutorial")

