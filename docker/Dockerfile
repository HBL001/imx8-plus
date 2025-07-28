#
# Dockerfile for Verdin iMX8M Plus (TorizonCore 6.8.3)
# C++ cross-compilation (no Qt) with SDL2 + OpenGL ES support
# (c) 2025 Richard Day – Highland Biosciences – DuoSight Project
# 
# Version 0.4 
#
# Fixed:  Free and non-free split
#

FROM torizon/cross-toolchain-arm64-imx8:4.6

ENV DEBIAN_FRONTEND=noninteractive
ENV LANG=en_US.UTF-8
ENV HOME=/home/torizon
ENV USER=torizon
ENV USE_CCACHE=1
ENV CCACHE_DIR=/home/torizon/.ccache
ENV DISPLAY=:0

WORKDIR /home/torizon

# ✅ Fix Bookworm non-free split
RUN echo "deb http://deb.debian.org/debian bookworm main contrib non-free non-free-firmware" > /etc/apt/sources.list && \
    echo "deb http://deb.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware" >> /etc/apt/sources.list && \
    echo "deb http://deb.debian.org/debian bookworm-updates main contrib non-free non-free-firmware" >> /etc/apt/sources.list

# ✅ Enable arm64 architecture and install cross-build dependencies
RUN dpkg --add-architecture arm64 && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
    libsdl2-dev:arm64 \
    libgles2-mesa-dev:arm64 \
    libegl1-mesa-dev:arm64 \
    libwayland-dev:arm64 \
    libxkbcommon-dev:arm64 \
    libinput-dev:arm64 \
    libdrm-dev:arm64 \
    libudev-dev:arm64 \
    libexpat1-dev:arm64 \
    libpng-dev:arm64 \
    cmake \
    make \
    g++ \
    git \
    pkg-config \
    rsync \
    vim \
    tmux \
    tree \
    locales \
    sudo && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Optional: workspace directory for development
RUN mkdir -p /opt/data/data_manager/{config,logs} && \
    chown -R torizon:torizon /opt/data

# Disable sshd (not needed in devcontainer)
RUN systemctl disable ssh || true && \
    rm -f /etc/service/sshd/run || true && \
    sed -i '/sshd/d' /etc/inittab || true

# Grant sudo access to torizon user
RUN echo 'torizon ALL=(ALL) NOPASSWD:ALL' > /etc/sudoers.d/torizon && \
    chmod 0440 /etc/sudoers.d/torizon

USER torizon
