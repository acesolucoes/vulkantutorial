cmake_minimum_required(VERSION 3.24)
project(Vulkan_examples)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Vulkan REQUIRED COMPONENTS glslc)

if(DEFINED Vulkan_FOUND)
    message(DEBUG "Vulkan FOUND")
else()
    message(FATAL_ERROR "NO Vulkan FOUND")
endif()

if(DEFINED Vulkan_GLSLC_EXECUTABLE)
    message(DEBUG "GLSLC FOUND")
else()
    message(FATAL_ERROR "NO GLSLC FOUND")
endif()

add_subdirectory(3rd-party/glfw)
include_directories(3rd-party/glfw/include)

add_subdirectory(3rd-party/glm)
add_subdirectory(src)