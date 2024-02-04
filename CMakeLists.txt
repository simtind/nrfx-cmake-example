
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
    GIT_TAG main
    OPTIONS 
        "NRFX_CONFIG_DIR ${CMAKE_CURRENT_LIST_DIR}/include")

project(nrfx-cmake-example LANGUAGES C CXX ASM)


# Get global settings from MDK

add_executable(exe src/main.c)

target_link_libraries(exe 
    PUBLIC
        nrf-mdk::startup
        nrf-mdk::definitions
        
        nrfx::hal
        nrfx::soc
        nrfx::drivers::prs
        nrfx::drivers::adc
        nrfx::drivers::bellboard
        nrfx::drivers::clock
        nrfx::drivers::comp
        nrfx::drivers::dppi
        nrfx::drivers::egu
        nrfx::drivers::gpiote
        nrfx::drivers::grtc
        nrfx::drivers::i2s
        nrfx::drivers::ipc
        nrfx::drivers::lpcomp
        nrfx::drivers::nfct
        nrfx::drivers::nvmc
        nrfx::drivers::pdm
        nrfx::drivers::power
        nrfx::drivers::ppi
        nrfx::drivers::pwm
        nrfx::drivers::qdec
        nrfx::drivers::qspi
        nrfx::drivers::rng
        nrfx::drivers::rramc
        nrfx::drivers::rtc
        nrfx::drivers::saadc
        nrfx::drivers::spi
        nrfx::drivers::spim
        nrfx::drivers::spis
        nrfx::drivers::systick
        nrfx::drivers::tbm
        nrfx::drivers::temp
        nrfx::drivers::timer
        nrfx::drivers::twi
        nrfx::drivers::twim
        nrfx::drivers::twis
        nrfx::drivers::uart
        nrfx::drivers::uarte
        nrfx::drivers::usbd
        nrfx::drivers::usbreg
        nrfx::drivers::vevif
        nrfx::drivers::wdt

        nrfx::helpers::ram_ctrl
        nrfx::helpers::gppi
        nrfx::helpers::flag32_allocator)

set_linker_script(exe ${MDK_SOURCE_LINKER_SCRIPT})

create_hex(exe)