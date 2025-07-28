FROM torizon/debian-imx8:4

ENV DEBIAN_FRONTEND=noninteractive

# Install system tools and build dependencies
RUN apt-get update && apt-get install -y \
    i2c-tools \
    spi-tools \
    python3 \
    python3-venv \
    python3-pip \
    python3-dev \
    build-essential \
    strace \
    gpiod \
    bsdmainutils \
    less \
    vim && \
    apt-get clean

# Create a clean Python venv
RUN python3 -m venv /opt/iotenv

# Install Python packages inside venv
RUN /opt/iotenv/bin/pip install --no-cache-dir smbus2 spidev

# Optional: create convenience aliases
RUN ln -s /opt/iotenv/bin/python /usr/local/bin/pyiot && \
    ln -s /opt/iotenv/bin/pip /usr/local/bin/pipiot && \
    ln -s /opt/iotenv/bin/activate /usr/local/bin/activate-iotenv

WORKDIR /home/torizon
CMD ["bash"]
