# Verdin I²C + GPIO Developer Container

This repository provides a custom Docker container for Torizon-based development on the **Toradex Verdin iMX8M Plus** platform. It includes tools for testing and interacting with I²C devices (e.g., MLX90640) and GPIO chips using standard Linux interfaces.

---

## 🧰 Features

This container builds on `torizon/debian-imx8:4` and includes:

- ✅ I²C support via `i2c-tools` and `python3-periphery`
- ✅ GPIO support via `libgpiod` and `gpiod`
- ✅ USB device detection (`usbutils`)
- ✅ General dev/debug tools:
  - `vim`, `less`, `htop`, `curl`, `net-tools`, `ping`
- ✅ Build tools: `build-essential`, `cmake`, `git`
- ✅ Python 3 + pip

---

## 📦 Build Instructions (on PC)

```bash
docker build -t clotspot/verdin-devtools:latest -f Dockerfile .
docker push clotspot/verdin-devtools:latest


## Run in on the target

docker run -it --rm \
  --privileged \
  --network host \
  -v /dev:/dev \
  --device-cgroup-rule='c 89:* rmw' \
  clotspot/verdin-devtools:latest


i2cdetect -y 3   # /dev/i2c-3 (verdin-i2c1)

gpiodetect
gpioinfo gpiochip0
