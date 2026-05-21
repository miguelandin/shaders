cmake_minimum_required(VERSION 3.15)
project(hello_window VERSION 1.0.0 LANGUAGES C CXX)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(OpenGL_GL_PREFERENCE GLVND)
find_package(OpenGL REQUIRED)

add_library(glad STATIC ../glad/src/gl.c)
target_include_directories(glad PUBLIC ../glad/include)

add_executable(hello_window src/main.cpp)
target_include_directories(hello_window PRIVATE src)
target_link_libraries(hello_window PRIVATE glfw OpenGL::GL glad)

add_custom_target(run
    COMMAND hello_window
    DEPENDS hello_window
    WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
)
