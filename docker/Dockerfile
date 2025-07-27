#
# Dockerfile for Verdin iMX8M Plus (TorizonCore 6.8.3)
# Qt5 + CMake cross-compilation + Python tools
# (C) Richard Day – Highland Biosciences – DuoSight Project
#

FROM torizon/cross-toolchain-arm64-imx8:4.6

ENV DEBIAN_FRONTEND=noninteractive
ENV LANG=en_US.UTF-8
ENV HOME=/home/torizon
ENV USER=torizon
ENV USE_CCACHE=1
ENV CCACHE_DIR=/home/torizon/.ccache
ENV QT_QPA_PLATFORM=wayland
ENV DISPLAY=:0

WORKDIR /home/torizon

# Enable aarch64 architecture and update package lists
RUN dpkg --add-architecture arm64 && \
    apt-get update

# Install Qt5 (GLES build), dev tools, and extra build essentials
RUN apt-get install -y \
    qtbase5-dev:arm64 \
    qtbase5-dev-tools:arm64 \
    qttools5-dev-tools:arm64 \
    qt5-qmake:arm64 \
    libqt5gui5:arm64 \
    libqt5core5a:arm64 \
    libgles-dev:arm64 \
    libqt5widgets5:arm64 \
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
    python3 \
    python3-pip \
    python3-numpy \
    python3-matplotlib \
 && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Optional data directories for runtime use
RUN mkdir -p /opt/data/data_manager/{config,logs} \
    && chown -R torizon:torizon /opt/data

# Disable SSH server inside the container
RUN systemctl disable ssh || true && \
    rm -f /etc/service/sshd/run || true && \
    sed -i '/sshd/d' /etc/inittab || true

USER torizon

