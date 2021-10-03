#
# @file firmware/CMakeLists.txt
#
cmake_minimum_required(VERSION 3.13)
INCLUDE(cmake/pico_sdk_import.cmake)
PROJECT(blink)

# ENABLE_LANGUAGE より後で実行すると
# rp2で利用するクロスコンパイラの指定が狂うため
# ENABLE_LANGUAGE 前に実行
pico_sdk_init()

ENABLE_LANGUAGE( C CXX ASM )
SET(CMAKE_C_STANDARD 11)
SET(CMAKE_C_STANDARD_REQUIRED ON)
SET(CMAKE_CXX_STANDARD 17)
SET(CMAKE_CXX_STANDARD_REQUIRED ON)

ADD_EXECUTABLE(hello
  hello.c
)
TARGET_LINK_LIBRARIES(hello pico_stdlib)
pico_enable_stdio_usb(hello 1)
pico_add_extra_outputs(hello)
