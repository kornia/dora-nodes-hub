# Dora Nodes Hub

A collection of [Dora](https://github.com/dora-rs/dora) dataflow nodes for computer vision pipelines using [Kornia-RS](https://github.com/kornia/kornia-rs).

## What's Inside

This repository contains ready-to-use Dora nodes for building computer vision applications:

- **Camera capture nodes** - Get video streams from webcams and IP cameras
- **Image processing nodes** - Apply filters and transformations to images  
- **Visualization nodes** - Display results in real-time viewers

## Usage

The nodes are designed to work together in dataflow pipelines. Build them with:

```bash
cargo build --release
```

Each node can be configured through environment variables and connected via Dora's dataflow system.

## Dependencies

Built with:
- [Dora](https://github.com/dora-rs/dora) - Dataflow runtime
- [Kornia-RS](https://github.com/kornia/kornia-rs) - Computer vision library
- [Rerun](https://rerun.io/) - Visualization platform

## License

Apache License 2.0 - see [LICENSE](LICENSE) for details.
