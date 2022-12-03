cmake_minimum_required(VERSION 3.12)

# Pull in SDK (must be before project)
include(pico-sdk/pico_sdk_init.cmake)
include(pico-sdk/external/pico_sdk_import.cmake)

project(dht_20_test C CXX ASM)
set(CMAKE_C_STANDARD 11)

if (PICO_SDK_VERSION_STRING VERSION_LESS "1.4.0")
    message(FATAL_ERROR "Raspberry Pi Pico SDK version 1.4.0 (or later) required. Your version is ${PICO_SDK_VERSION_STRING}")
endif()

# Initialize the SDK
pico_sdk_init()

add_compile_options(-Wall
        -Wno-format          # int != int32_t as far as the compiler is concerned because gcc has int32_t as long int
        -Wno-unused-function # we have some for the docs that aren't called
        -Wno-maybe-uninitialized
        )

add_executable(dht20_pico_example
    dht20_pico_example.c
)

add_subdirectory("dht20-pico")
target_include_directories(dht20 PUBLIC "dht20-pico")
target_link_directories(dht20 PUBLIC "dht20-pico")

target_link_libraries(dht20_pico_example pico_stdlib hardware_i2c pico_binary_info dht20)

pico_enable_stdio_usb(dht20_pico_example 1)
pico_enable_stdio_uart(dht20_pico_example 0)

pico_add_extra_outputs(dht20_pico_example)
