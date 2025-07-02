# Kornia GStreamer Capture Node

A [Dora](https://github.com/dora-rs/dora) node for capturing video frames from webcams and RTSP streams using GStreamer through [Kornia-RS](https://github.com/kornia/kornia-rs).

## Overview

This node captures video frames from various sources and outputs them as RGB8 images. It supports both local webcam capture via V4L2 and remote RTSP stream capture, making it suitable for a wide range of computer vision applications.

## Configuration

The node is configured through environment variables:

### Required Variables

- `SOURCE_TYPE` - Type of video source (`"webcam"` or `"rtsp"`)
- `SOURCE_URI` - Source identifier (device path for webcam, URL for RTSP)

### Webcam-specific Variables (when SOURCE_TYPE="webcam")

- `IMAGE_COLS` - Frame width in pixels (e.g., `640`)
- `IMAGE_ROWS` - Frame height in pixels (e.g., `480`)
- `SOURCE_FPS` - Capture framerate (e.g., `30`)

### Example Configurations

#### Webcam Capture
```bash
export SOURCE_TYPE="webcam"
export SOURCE_URI="/dev/video0"
export IMAGE_COLS="640"
export IMAGE_ROWS="480"
export SOURCE_FPS="30"
```

#### RTSP Stream
```bash
export SOURCE_TYPE="rtsp"
export SOURCE_URI="rtsp://admin:password@192.168.1.100:554/stream1"
```

### Integration in Dora Dataflow

```yaml
nodes:
  - id: camera
    build: cargo build -p kornia-gst-capture --release
    path: target/release/kornia-gst-capture
    inputs:
      tick: dora/timer/millis/30
    outputs:
      - frame
    env:
      SOURCE_TYPE: "webcam"
      SOURCE_URI: "/dev/video0"
      IMAGE_COLS: "640"
      IMAGE_ROWS: "480"
      SOURCE_FPS: "30"
```

## System Requirements

### GStreamer Installation

Ubuntu/Debian:
```bash
sudo apt-get install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev
```