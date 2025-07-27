#
# (c) 2025 Highland Biosciences Limited - Scotland
#
# Dr Richard Day
#
# Extended Developer Container for Verdin iMX8M Plus
# Includes: I2C, GPIO, USB, dev tools, Python, debugging
#
# Build: docker build -t clotspot/verdin-devtools:latest -f Dockerfile .
#
# Run it: docker run -it --rm \
#  -v /dev:/dev \
#  --device-cgroup-rule='c 89:* rmw' \
#  --privileged \
#  --network host \
#  clotspot/verdin-devtools:latest
#
#

FROM torizon/debian-imx8:4

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    i2c-tools \
    python3 \
    python3-pip \
    python3-periphery \
    libgpiod2 \
    libgpiod-dev \
    gpiod \
    usbutils \
    pciutils \
    vim \
    less \
    htop \
    curl \
    net-tools \
    iputils-ping \
    git \
    sudo \
    build-essential \
    cmake \
    && apt-get clean

# Optional: symlink python -> python3
RUN ln -sf /usr/bin/python3 /usr/bin/python

# Default shell
CMD [ "bash" ]
