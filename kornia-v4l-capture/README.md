# Kornia V4L Capture Node

A [Dora](https://github.com/dora-rs/dora) dataflow node for capturing video frames from V4L2 (Video4Linux2) devices using [Kornia-RS](https://github.com/kornia/kornia-rs).

## Overview

This node interfaces with V4L2 compatible devices (webcams, USB cameras, etc.) to capture video frames and stream them through the Dora dataflow system. It's designed to work as a source node in computer vision pipelines.

**Note**: This node is Linux-only as it uses the Video4Linux2 (V4L2) API which is specific to Linux systems.

### Installing Prerequisites

On Ubuntu/Debian:
```bash
sudo apt-get update
sudo apt-get install clang libv4l-dev v4l-utils
```

## Configuration

The node is configured through environment variables:

| Variable | Description | Example | Required |
|----------|-------------|---------|----------|
| `SOURCE_DEVICE` | V4L2 device path | `/dev/video0` | Yes |
| `IMAGE_COLS` | Frame width in pixels | `640` | Yes |
| `IMAGE_ROWS` | Frame height in pixels | `480` | Yes |
| `SOURCE_FPS` | Frames per second | `30` | Yes |
| `PIXEL_FORMAT` | Pixel format (`YUYV` or `MJPG`) | `YUYV` | Yes |

## Usage Example

### Environment Setup

```bash
export SOURCE_DEVICE="/dev/video0"
export IMAGE_COLS="640"
export IMAGE_ROWS="480"
export SOURCE_FPS="30"
export PIXEL_FORMAT="YUYV"
```

### Integration in Dora Dataflow

```yaml
nodes:
  - id: camera_capture
    build: cargo build -p kornia-v4l-capture --release
    path: target/release/kornia-v4l-capture
    inputs:
      tick: dora/timer/millis/30
    outputs:
      - frame
    env:
      SOURCE_DEVICE: "/dev/video0"
      IMAGE_COLS: 640
      IMAGE_ROWS: 480
      SOURCE_FPS: 30
      PIXEL_FORMAT: "YUYV"
```

## Troubleshooting

### Common Issues

1. **Platform not supported**: This node only works on Linux systems
   ```bash
   uname -s  # Should return "Linux"
   ```

2. **Build failures**: Ensure clang is installed
   ```bash
   clang --version  # Should show clang version
   ```

3. **Device not found**: Check that the device path exists and is accessible
   ```bash
   ls -la /dev/video*
   ```

4. **Permission denied**: Ensure user has access to video devices
   ```bash
   sudo usermod -a -G video $USER
   ```

5. **Format not supported**: Verify your camera supports the specified pixel format
   ```bash
   v4l2-ctl --device=/dev/video0 --list-formats
   ```

6. **Resolution not supported**: Check supported resolutions
   ```bash
   v4l2-ctl --device=/dev/video0 --list-framesizes=YUYV
   ```