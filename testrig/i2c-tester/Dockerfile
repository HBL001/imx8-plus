
#
# (c) 2025 Highland Biosciences Limited - Scotland
#
# Bringup Test Harness for I2C-1 on the imx8x Plus
#
# build me: docker build -t clotspot/verdin-i2c-gpio:latest -f Dockerfile .
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
    && apt-get clean

# Ensure 'python' points to 'python3'
RUN ln -sf /usr/bin/python3 /usr/bin/python

# Default command
CMD [ "bash" ]

