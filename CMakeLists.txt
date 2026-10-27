cmake_minimum_required(VERSION 3.21)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release")
endif()

project(android-app-sdl3-image-webp-opengl-cpp CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# -----------------------------------------------------------------------------
# Paths
# -----------------------------------------------------------------------------
set(SDL3_DIR       "C:/libs/sdl3-3.4.18-android")
set(SDL3_IMAGE_DIR "C:/libs/sdl3_image-3.4.8-webp-android")

# -----------------------------------------------------------------------------
# Native Shared Library Target
# -----------------------------------------------------------------------------
add_library(main SHARED
    src/main.cpp
)

# -----------------------------------------------------------------------------
# Include Directories
# -----------------------------------------------------------------------------
target_include_directories(main PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/src
    ${SDL3_DIR}/${ANDROID_ABI}/include
    ${SDL3_IMAGE_DIR}/${ANDROID_ABI}/include
)

# -----------------------------------------------------------------------------
# Link SDL3, SDL3_image & Android System Libraries
# -----------------------------------------------------------------------------
target_link_libraries(main PRIVATE
    ${SDL3_IMAGE_DIR}/${ANDROID_ABI}/lib/libSDL3_image.so
    ${SDL3_DIR}/${ANDROID_ABI}/lib/libSDL3.so
    GLESv3
    EGL
    android
    log
)
