cmake_minimum_required(VERSION 3.13)
set(CMAKE_TOOLCHAIN_FILE ${CMAKE_CURRENT_SOURCE_DIR}/../../cmake/stm32_gcc.cmake)
set(STM32_CUBE_L4_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../../../STM32CubeL4)

project(stm32-blinky C ASM)
set(CMAKE_INCLUDE_CURRENT_DIR TRUE)

find_package(CMSIS COMPONENTS STM32L4 REQUIRED)
find_package(HAL COMPONENTS STM32L4 RCC GPIO CORTEX REQUIRED)
# Find all drivers:
#find_package(HAL COMPONENTS STM32L0 STM32F1 STM32F4 REQUIRED)
# Find drivers for all families:
#find_package(HAL COMPONENTS RCC GPIO CORTEX REQUIRED)
# Find LL driver:
#find_package(HAL COMPONENTS LL_GPIO REQUIRED)
# Find everything:
#find_package(HAL REQUIRED)

# STM32F4-Discovery
add_executable(stm32-blinky-l4 blinky.c stm32l4xx_hal_conf.h)
target_link_libraries(stm32-blinky-l4 
    HAL::STM32::L4::RCC
    HAL::STM32::L4::GPIO
    HAL::STM32::L4::CORTEX
    CMSIS::STM32::L4P5VG
    STM32::NoSys 
)
