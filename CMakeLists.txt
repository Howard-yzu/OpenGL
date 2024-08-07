cmake_minimum_required(VERSION 3.10)
project(OpenGL)

set(CMAKE_CXX_STANDARD 11)

# Include directories
include_directories(${CMAKE_SOURCE_DIR}/include)
include_directories(${CMAKE_SOURCE_DIR}/external/glad/include)
include_directories(${CMAKE_SOURCE_DIR}/external/glfw/include)
include_directories(${CMAKE_SOURCE_DIR}/external/glm)

# Add GLFW
add_subdirectory(external/glfw)

# Add glad source
set(GLAD_SRC ${CMAKE_SOURCE_DIR}/external/glad/src/glad.c)

# Function to add a tutorial
function(add_tutorial tutorial_name)
    file(GLOB TUTORIAL_SOURCES
        ${CMAKE_SOURCE_DIR}/src/${tutorial_name}/*.cpp
    )
    add_executable(${tutorial_name} ${TUTORIAL_SOURCES} ${GLAD_SRC})
    target_link_libraries(${tutorial_name} glfw ${GLFW_LIBRARIES})
    target_include_directories(${tutorial_name} PRIVATE ${CMAKE_SOURCE_DIR}/external/glm)
endfunction()

# Add each tutorial
add_tutorial(Hello_Triangle)
add_tutorial(Shaders)
add_tutorial(Textures)
add_tutorial(Transformations)
add_tutorial(Camera)
add_tutorial(Colors)
add_tutorial(Basic_Lighting)
add_tutorial(Materials)
add_tutorial(Lighting_maps)
add_tutorial(Light_casters)
add_tutorial(Multiple_lights)