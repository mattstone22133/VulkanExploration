cmake_minimum_required(VERSION 3.18 FATAL_ERROR)

set(EXECUTABLE_NAME VulkanTutorial)


project("${EXECUTABLE_NAME}")
file(GLOB_RECURSE sources CONFIGURE_DEPENDS src/*.cpp src/*.h)
add_executable(${EXECUTABLE_NAME} ${sources})

#NOTE: macOS: After installing Vulkan SDK, you must have environment variable pointing to the SDK lcation. see https://github.com/KhronosGroup/MoltenVK/issues/116
# VULKAN_SDK=/path/to/vulkansdk/macOS
# I added the above to my ~/.bash_profile, but on mac I needed to restart the computer before it would be detected by vscode (even after clearing cmake cache)
#NOTE: Vulkan is not all capitalized, and the generated variables are not all caplital.
find_package(Vulkan REQUIRED)
message("VULKAN_FOUND: " ${VULKAN_FOUND})
message("Vulkan_LIBRARY: " ${Vulkan_LIBRARY})
message("Vulkan_INCLUDE_DIR: " ${Vulkan_INCLUDE_DIR})
target_include_directories(${EXECUTABLE_NAME}
    PUBLIC ${Vulkan_INCLUDE_DIR})
target_link_libraries(${EXECUTABLE_NAME} PUBLIC ${Vulkan_LIBRARY})

set_target_properties(${EXECUTABLE_NAME} PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED YES
    CXX_EXTENSIONS NO)

include(${SHARED_CMAKE_UTILITES_DIR}/LinkGLFW.cmake) 
LinkGLFW(${EXECUTABLE_NAME} PUBLIC)

include(${SHARED_CMAKE_UTILITES_DIR}/LinkGLM.cmake) 
LinkGLM(${EXECUTABLE_NAME} PUBLIC)