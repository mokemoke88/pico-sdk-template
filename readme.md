# Raspberry PI Pico SDK 開発用 テンプレート

VSCode Dev Container 拡張を使用して
Pico SDK を使用した Raspberry PI Pico の開発環境を構築するための
テンプレート プロジェクト

## 環境

VSCode Dev Container 拡張
Docker for Windows (WSL2)

## 

ベースイメージ: debian:bullseye-slim

- /opt/pico-sdk 以下に 最新版の Pico SDK (https://github.com/raspberrypi/pico-sdk.git)

- /opt/pico-example 以下に Pico Example (https://github.com/raspberrypi/pico-examples.git)

を格納

設定済み環境変数

PICO_SDK_PATH=/opt/pico-sdk

詳細は .devcontainer/Dockerfile を参照

## 利用前

/opt/pico-example/pico_sdk_import.cmake を持ってくること.

** サンプルプロジェクトの場合 firmware/cmake 以下にコピーする.

## CMakeLists.txt 雛型

```cmake
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
```
