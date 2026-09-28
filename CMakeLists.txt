# Must strictly be the first line
cmake_minimum_required(VERSION 3.20)

project(MyProject LANGUAGES C CXX)

# Specify C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Prefer modern GLVND OpenGL libraries over legacy GL on Linux (fixes CMP0072 warning)
set(OpenGL_GL_PREFERENCE GLVND)
find_package(OpenGL REQUIRED)

# Configure GLFW options before adding its directory
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_INSTALL OFF CACHE BOOL "" FORCE)

# Add GLFW dependency directory
add_subdirectory(external/glfw)

# Add application executable
add_executable(${PROJECT_NAME} src/main.cpp)

# Link dependencies
target_link_libraries(${PROJECT_NAME} 
    PRIVATE 
        glfw 
        OpenGL::GL
)

target_include_directories(${PROJECT_NAME} PRIVATE external/glfw/include)