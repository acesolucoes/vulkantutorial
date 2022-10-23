cmake_minimum_required(VERSION 3.24)
project(Vulkan_examples_src)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if(WIN32)
    # https://stackoverflow.com/questions/27442885/syntax-error-with-stdnumeric-limitsmax
    add_definitions(-DNOMINMAX)
endif()

add_executable(Base base.cpp)
target_link_libraries(Base Vulkan::Vulkan)
target_include_directories(Base PRIVATE Vulkan::Headers)
target_link_libraries(Base glfw ${GLFW_LIBRARIES})
target_link_libraries(Base glm::glm)

add_executable(Main1 maincode.cpp)
target_link_libraries(Main1 Vulkan::Vulkan)
target_include_directories(Main1 PRIVATE Vulkan::Headers)
target_link_libraries(Main1 glfw ${GLFW_LIBRARIES})
target_link_libraries(Main1 glm::glm)

add_executable(WindowsSurface maincode.cpp)
target_link_libraries(WindowsSurface Vulkan::Vulkan)
target_include_directories(WindowsSurface PRIVATE Vulkan::Headers)
target_link_libraries(WindowsSurface glfw ${GLFW_LIBRARIES})
target_link_libraries(WindowsSurface glm::glm)

add_custom_command( TARGET Main1 POST_BUILD
                    COMMAND ${Vulkan_GLSLC_EXECUTABLE} simple.vert -o vert.spv
                    COMMAND ${Vulkan_GLSLC_EXECUTABLE} simple.frag -o frag.spv
                    WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}/shaders
                    COMMENT "compiling" )