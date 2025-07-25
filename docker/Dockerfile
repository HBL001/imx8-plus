#
# Dockerfile for Verdin iMX8M Plus (TorizonCore 6.8.3)
# Supports: C++ sensor logic + Python GUI with PyQt5 or OpenCV over HDMI
#
# (c) Richard Day - Highland Biosciences - DuoSight Project
#

FROM torizon/debian-cross-toolchain-ssh-arm64:2-bullseye

ENV DEBIAN_FRONTEND=noninteractive
ENV LANG=en_US.UTF-8
ENV HOME=/home/torizon
ENV USER=torizon
ENV USE_CCACHE=1
ENV CCACHE_DIR=/home/torizon/.ccache
ENV QT_QPA_PLATFORM=wayland
ENV DISPLAY=:0

WORKDIR /home/torizon

# Update and install general dev tools
RUN apt-get update && apt-get install -y \
    cmake \
    make \
    git \
    g++ \
    pkg-config \
    rsync \
    vim \
    tmux \
    tree \
    locales \
    sudo \
# Add Python + scientific + GUI libraries
    python3 \
    python3-pip \
    python3-numpy \
    python3-matplotlib \
    python3-opencv \
    python3-pyqt5 \
# ARM64 dev headers for C++ cross builds
    libgpiod-dev:arm64 \
    libsqlite3-dev:arm64 \
    libopencv-dev:arm64 \
    libdrm-dev:arm64 \
    libegl1-mesa-dev:arm64 \
    libgles2-mesa-dev:arm64 \
    libwayland-dev:arm64 \
    libudev-dev:arm64 \
    libinput-dev:arm64 \
    libnn-imx-dev:arm64 \
    libvsi-nn-dev:arm64 \
    qtbase5-dev:arm64 \
    qttools5-dev-tools:arm64 \
    qtwayland5:arm64 \
    libqt5gui5:arm64 \
    libqt5widgets5:arm64 \
    libqt5network5:arm64 \
 && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Optional: Create working dirs
RUN mkdir -p /opt/data/data_manager/{config,logs} \
    && chown -R torizon:torizon /opt/data

USER torizon
