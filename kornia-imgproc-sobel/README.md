# Kornia Imgproc Sobel Node

A [Dora](https://github.com/dora-rs/dora) dataflow node for real-time Sobel edge detection using [Kornia-RS](https://github.com/kornia/kornia-rs).

## Overview

This node applies Sobel edge detection to incoming image frames, highlighting edges and boundaries in the image.

## Usage

```yaml
nodes:
  - id: sobel_filter
    build: cargo build -p kornia-imgproc-sobel --release  
    path: target/release/kornia-imgproc-sobel
    inputs:
      frame: v4l-capture/frame
    outputs:
      - output
```

## Configuration

The node automatically adapts to incoming frame dimensions and encoding. No additional configuration is required.

## Algorithm Details

- **Sobel operator**: 3x3 kernel for edge detection
- **Color conversion**: YUYV converted using BT.601 Full range
- **Output format**: Float32 Sobel values mapped to U8 range

## Dependencies

- [dora-node-api](https://crates.io/crates/dora-node-api) - Dora runtime integration
- [kornia-image](https://github.com/kornia/kornia-rs) - Image data structures
- [kornia-imgproc](https://github.com/kornia/kornia-rs) - Image processing operations
- [kornia-io](https://github.com/kornia/kornia-rs) - JPEG decoding

## Examples

See the parent [dora-nodes-hub](../README.md) for complete pipeline examples using this node.

## License

Apache License 2.0 - see [LICENSE](../LICENSE) for details.
