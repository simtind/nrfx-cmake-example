
cmake_minimum_required(VERSION 3.6)

# Get CPM
file(
  DOWNLOAD
  https://github.com/cpm-cmake/CPM.cmake/releases/download/v0.38.3/CPM.cmake
  ${CMAKE_CURRENT_BINARY_DIR}/cmake/CPM.cmake
  EXPECTED_HASH SHA256=cc155ce02e7945e7b8967ddfaff0b050e958a723ef7aad3766d368940cb15494
)
include(${CMAKE_CURRENT_BINARY_DIR}/cmake/CPM.cmake)

# Get nrfx-cmake and nrf-mdk
CPMAddPackage(
    NAME nrfx-cmake
    GITHUB_REPOSITORY simtind/nrfx-cmake
    GIT_TAG main)
    
project(nrfx-cmake-example LANGUAGES C CXX ASM)


# Get global settings from MDK

add_executable(exe src/main.c)

target_link_libraries(exe 
    PUBLIC
        nrf-mdk::startup
        nrf-mdk::definitions
        
        nrfx::hal
        nrfx::soc
        nrfx::drivers
        nrfx::helpers)

set_linker_script(exe ${MDK_SOURCE_LINKER_SCRIPT})

create_hex(exe)