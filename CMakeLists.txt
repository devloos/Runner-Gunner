cmake_minimum_required(VERSION 3.15)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_BUILD_TYPE Debug)

project(main)

include_directories(main PUBLIC include)
add_executable(${PROJECT_NAME} src/main.cpp src/memory/initRaylib.cpp
               src/memory/initRect.cpp src/memory/initTextures.cpp
               src/memory/deallocation.cpp src/handlers/gameLoop.cpp 
               src/handlers/logic.cpp src/handlers/handleClouds.cpp
               src/updateRenderer.cpp src/sprite.cpp)

find_library(raylib raylib PATHS lib)
include_directories(${PROJECT_NAME} PUBLIC include/raylib)
target_link_libraries(${PROJECT_NAME} ${raylib})

# Checks if OSX and links appropriate frameworks (only required on MacOS)
if (APPLE)
    target_link_libraries(${PROJECT_NAME} "-framework IOKit")
    target_link_libraries(${PROJECT_NAME} "-framework Cocoa")
    target_link_libraries(${PROJECT_NAME} "-framework OpenGL")
endif()
