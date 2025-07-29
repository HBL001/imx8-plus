#
# Dockerfile for Verdin iMX8M Plus (TorizonCore 6.8.3)
# C++ cross-compilation with SDL2 + OpenGL ES support
# (c) 2025 Richard Day – Highland Biosciences – DuoSight Project
#
# Version 0.9
# -------------------------------------------------------------------
# ✅ Fixed: Bookworm 'non-free' and 'non-free-firmware' split in APT
# ✅ Fixed: SDL2 header squiggle errors in VSCode (headers now copied)
# ✅ Fixed: SDL2 linker errors (libSDL2*.so copied into sysroot)
# ✅ Fixed: EGL and GLESv2 runtime linking errors (libEGL*.so, libGLESv2*.so)
# ✅ Fixed: Missing pkgconfig .pc files for SDL2 in sysroot
# ✅ Aligned PKG_CONFIG_PATH and sysroot structure for proper pkg-config detection
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

# ✅ Fix Bookworm non-free split for firmware and SDL2 availability
RUN echo "deb http://deb.debian.org/debian bookworm main contrib non-free non-free-firmware" > /etc/apt/sources.list && \
    echo "deb http://deb.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware" >> /etc/apt/sources.list && \
    echo "deb http://deb.debian.org/debian bookworm-updates main contrib non-free non-free-firmware" >> /etc/apt/sources.list

# ✅ Install all runtime and cross-dev dependencies (arm64)
RUN dpkg --add-architecture arm64 && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
    libsdl2-dev:arm64 \
    libgles2-mesa-dev:arm64 \
    libegl1-mesa-dev:arm64 \
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

# ✅ Inject SDL2 + GLESv2 + EGL headers, libraries, and pkgconfig into Yocto SDK sysroot
RUN mkdir -p \
      /usr/local/oecore-x86_64/sysroots/aarch64-tdx-linux/usr/include/SDL2 \
      /usr/local/oecore-x86_64/sysroots/aarch64-tdx-linux/usr/lib \
      /usr/local/oecore-x86_64/sysroots/aarch64-tdx-linux/usr/lib/pkgconfig && \
    cp -r /usr/include/SDL2/* /usr/local/oecore-x86_64/sysroots/aarch64-tdx-linux/usr/include/SDL2/ && \
    cp /usr/lib/aarch64-linux-gnu/libSDL2*.so* /usr/local/oecore-x86_64/sysroots/aarch64-tdx-linux/usr/lib/ && \
    cp /usr/lib/aarch64-linux-gnu/libGLESv2*.so* /usr/local/oecore-x86_64/sysroots/aarch64-tdx-linux/usr/lib/ && \
    cp /usr/lib/aarch64-linux-gnu/libEGL*.so* /usr/local/oecore-x86_64/sysroots/aarch64-tdx-linux/usr/lib/ && \
    cp /usr/lib/aarch64-linux-gnu/pkgconfig/sdl2.pc /usr/local/oecore-x86_64/sysroots/aarch64-tdx-linux/usr/lib/pkgconfig/

# Optional: development data workspace
RUN mkdir -p /opt/data/data_manager/{config,logs} && \
    chown -R torizon:torizon /opt/data

# Disable sshd (not needed in devcontainer)
RUN systemctl disable ssh || true && \
    rm -f /etc/service/sshd/run || true && \
    sed -i '/sshd/d' /etc/inittab || true

# Allow passwordless sudo for the dev user
RUN echo 'torizon ALL=(ALL) NOPASSWD:ALL' > /etc/sudoers.d/torizon && \
    chmod 0440 /etc/sudoers.d/torizon

USER torizon
