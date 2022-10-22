# Generated Cmake Pico project file

cmake_minimum_required(VERSION 3.13)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# Initialise pico_sdk from installed location
# (note this can come from environment, CMake cache etc)
set(PICO_SDK_PATH "/home/maxime/pico/pico-sdk")

# Pull in Raspberry Pi Pico SDK (must be before project)
include(pico_sdk_import.cmake)

project(uxn-dfu C CXX ASM)

# Initialise the Raspberry Pi Pico SDK
pico_sdk_init()

# Add executable. Default name is the project name, version 0.1

add_executable(uxn-dfu 
    uxn-dfu.c
    usb_descriptors.c
    uxn.c
    devices/system.c
    devices/datetime.c
)

target_include_directories(uxn-dfu PUBLIC
      ${CMAKE_CURRENT_LIST_DIR})

pico_set_program_name(uxn-dfu "uxn-dfu")
pico_set_program_version(uxn-dfu "0.1")

pico_enable_stdio_uart(uxn-dfu 1)
pico_enable_stdio_usb(uxn-dfu 0)

# Add the standard library to the build
target_link_libraries(uxn-dfu 
    pico_stdlib
    tinyusb_device
    tinyusb_board
)

pico_add_extra_outputs(uxn-dfu)

