cmake_minimum_required(VERSION 3.17)

project(tv-test C CXX ASM)


# CMake options
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_VERBOSE_MAKEFILE ON)


include(.cmake/common.cmake)
# Framework нам пока не нужен
# include(.cmake/framework.cmake)

# Настройка TurboVision под терминал
#if(STM32)
    set(TV_TERMINAL 1)
    set(TV_BARE 1)
#endif()

set(TV_NO_FILESYSTEM 1)



# Подсасываем библиотеки
add_subdirectory("${LIB_ROOT}/tvision")
# add_subdirectory("${LIB_ROOT}/umba")


# C/C++ language settings
# https://matgomes.com/setting-cpp-standard-cmake/
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED On)
set(CMAKE_C_EXTENSIONS Off)
set(CMAKE_CXX_EXTENSIONS Off)


set(COMMON_LIBS tvision::tvision)

include_directories(${LIB_ROOT})

# Project include paths
set(INCLUDES
)

set(EXAMPLES ${LIB_ROOT}/tvision/tvision/examples)

set(SOURCES # test.cpp
#    tvision/examples/progba/example.cpp
#    tvision/examples/progba/makerez.cpp
#    tvision/examples/progba/readrez.cpp
#    tvision/examples/progba/tprogbar.cpp
)


if(STM32)
endif()  # STM32

# https://stackoverflow.com/questions/11944060/how-to-detect-target-architecture-using-cmake
message("Target Processor: " ${CMAKE_SYSTEM_PROCESSOR})
message("Host Processor  : " ${CMAKE_HOST_SYSTEM_PROCESSOR})
 


add_compile_definitions(${TV_DEFINITIONS})

add_executable(example ${EXAMPLES}/progba/example.cpp ${EXAMPLES}/progba/tprogbar.cpp )
fw_add_target_options(example "UNICODE" "CONSOLE" "BIGOBJ"
                              #"BIN" "HEX"
                              # "FLASH"
                              )
target_link_libraries(example PRIVATE "${COMMON_LIBS}")


add_executable(makerez ${EXAMPLES}/progba/makerez.cpp ${EXAMPLES}/progba/tprogbar.cpp )
fw_add_target_options(makerez "UNICODE" "CONSOLE" "BIGOBJ"
                              #"BIN" "HEX"
                              # "FLASH"
                              )
target_link_libraries(makerez PRIVATE "${COMMON_LIBS}")


add_executable(readrez ${EXAMPLES}/progba/readrez.cpp ${EXAMPLES}/progba/tprogbar.cpp )
fw_add_target_options(readrez "UNICODE" "CONSOLE" "BIGOBJ"
                              #"BIN" "HEX"
                              # "FLASH"
                              )
target_link_libraries(readrez PRIVATE "${COMMON_LIBS}")




# target_include_directories(${PROJECT_NAME} PRIVATE ${INCLUDES})

# target_compile_definitions(${PROJECT_NAME} PRIVATE "ES_4007_BMCL")
# target_compile_definitions(${PROJECT_NAME} PRIVATE "FIRMWARE_TEST_MODE")

# target_link_libraries(${PROJECT_NAME} PRIVATE "${COMMON_LIBS}")

# if(STM32)
#     # Настраиваем TheFramework
#     target_link_options(${PROJECT_NAME} PRIVATE "-Wl,--defsym=FW_HDR_FLAGS=0x7")
#     
#     # Настраиваем раскладку флешки/срама
#     target_compile_definitions(${PROJECT_NAME} PRIVATE "flash_layout")
#     target_compile_definitions(${PROJECT_NAME} PRIVATE "sram_layout")
#     
#     # Настраиваем тактирование
#     target_compile_definitions(${PROJECT_NAME} PRIVATE "HSE_VALUE=16000000" "MCU_PLL_M=16" "MCU_PLL_Q=7" "MCU_PLL_N=360" "MCU_PLL_P=2")
# endif()










