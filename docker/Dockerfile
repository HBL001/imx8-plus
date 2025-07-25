#
# Dockerfile for Verdin iMX8M Plus (TorizonCore 6.8.3)
# (C) Richard Day – Highland Biosciences – DuoSight Project
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

RUN apt-get update && apt-get install -y \
    # General development tools
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
    # Python 3 + non-GUI data tools
    python3 \
    python3-pip \
    python3-numpy \
    python3-matplotlib \
 && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Optional: Create persistent working dirs
RUN mkdir -p /opt/data/data_manager/{config,logs} \
    && chown -R torizon:torizon /opt/data

USER torizon
