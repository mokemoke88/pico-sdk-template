FROM debian:bullseye-slim

RUN apt update \
    && apt install -y sudo cmake gcc-arm-none-eabi libnewlib-arm-none-eabi build-essential git python3 \
    && apt clean \
    && rm -rf /var/lib/apt/lists/* \
    && mkdir -p /opt \
    && cd /opt \
    && git clone -b master https://github.com/raspberrypi/pico-sdk.git \
    && cd pico-sdk \
    && git submodule update --init \
    && git pull \
    && git submodule update \
    && cd .. \
    && git clone -b master https://github.com/raspberrypi/pico-examples.git

ENV PICO_SDK_PATH=/opt/pico-sdk

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

USER $USERNAME
