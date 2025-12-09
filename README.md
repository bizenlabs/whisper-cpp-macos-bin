# whisper.cpp macOS Binary Distributions

Pre-built binary distributions of [whisper.cpp](https://github.com/ggml-org/whisper.cpp) for macOS with optimized builds for both Apple Silicon and Intel architectures.

## 🚀 Quick Start

### Download Pre-built Binaries

Visit the [Releases](https://github.com/bizenlabs/whisper-cpp-macos-bin/releases) page to download the latest builds:

- **Apple Silicon (M1/M2/M3/M4)**: `whisper-cpp-*-macos-arm64-metal.tar.gz`
  - Includes Metal GPU acceleration for optimal performance
  - Optimized with ARM NEON and Accelerate framework
  
- **Intel (x86_64)**: `whisper-cpp-*-macos-x86_64-accelerate.tar.gz`
  - CPU-optimized with AVX/AVX2 instructions
  - Uses Accelerate framework for performance

### Usage

```bash
# 1. Download and extract the appropriate binary for your architecture
tar -xzf whisper-cpp-*.tar.gz
cd whisper-cpp-*

# 2. Download a model
cd models
./download-ggml-model.sh base.en

# 3. Transcribe audio
cd ..
./bin/whisper-cli -m models/ggml-base.en.bin -f samples/jfk.wav
```

## 📋 System Requirements

- **macOS**: 11.0 (Big Sur) or later
- **Apple Silicon builds**: Requires Apple M-series processor
- **Intel builds**: Requires x86_64 Intel processor

## 🔧 Build Configurations

### Apple Silicon (ARM64) - Metal GPU

This build is optimized for Apple Silicon Macs and includes:
- ✅ **Metal GPU acceleration** - Utilizes Apple's GPU for faster inference
- ✅ **ARM NEON** - ARM-specific SIMD optimizations
- ✅ **Accelerate framework** - Apple's optimized math library
- ✅ **Native ARM64** - No Rosetta 2 translation needed

**Performance**: Best performance on M1/M2/M3/M4 Macs with significant GPU acceleration.

### Intel (x86_64) - Accelerate

This build is optimized for Intel Macs and includes:
- ✅ **AVX/AVX2** - Advanced vector extensions for faster CPU processing
- ✅ **Accelerate framework** - Apple's optimized math library
- ✅ **F16C** - Half-precision floating point support
- ❌ No GPU acceleration (CPU only)

**Performance**: Optimized CPU performance on Intel Macs.

## 🛠️ Building From Source

This repository contains GitHub Actions workflows that automatically build whisper.cpp binaries.

### Automatic Builds

Builds are triggered:
1. **Tag-based releases**: Push a tag starting with `v*` (e.g., `v1.8.2`)
2. **Manual workflow dispatch**: Trigger builds manually from the Actions tab

### Manual Build Trigger

To trigger a build manually:

1. Go to the [Actions](https://github.com/bizenlabs/whisper-cpp-macos-bin/actions) tab
2. Select "Build and Release whisper.cpp macOS Binaries"
3. Click "Run workflow"
4. Enter:
   - **whisper.cpp version**: The version/tag from [whisper.cpp](https://github.com/ggml-org/whisper.cpp) to build (e.g., `v1.8.2`, `master`)
   - **Release tag**: The tag for this release in your repo (e.g., `v1.8.2-1`)
5. Click "Run workflow"

### Build Matrix

The workflow builds two configurations in parallel:

| Configuration | OS | Architecture | GPU Support | Optimizations |
|--------------|-----|--------------|-------------|---------------|
| macOS ARM64 (Metal) | macOS 14 (Sonoma) | arm64 | Metal GPU | ARM NEON, Accelerate |
| macOS x86_64 (Accelerate) | macOS 14 (cross-compile) | x86_64 | None (CPU) | AVX/AVX2, Accelerate |

## 📦 Release Contents

Each release includes:

```
whisper-cpp-<version>-<platform>/
├── bin/                          # Compiled binaries
│   ├── whisper-cli              # Main CLI tool
│   ├── whisper-bench            # Benchmarking tool
│   ├── whisper-stream           # Real-time streaming
│   ├── whisper-server           # HTTP API server
│   └── ...                      # Additional tools
├── models/                       # Model download scripts
│   ├── download-ggml-model.sh
│   └── download-vad-model.sh
├── samples/                      # Sample audio files
├── README.txt                    # Quick start guide
├── README.md                     # Full documentation
└── LICENSE                       # License file
```

## 🔍 Verifying Downloads

Each release includes SHA256 checksums. Verify your download:

```bash
shasum -a 256 -c whisper-cpp-*.tar.gz.sha256
```

## 🎯 Available Tools

- **whisper-cli** - Command-line transcription tool
- **whisper-bench** - Performance benchmarking
- **whisper-stream** - Real-time audio transcription from microphone
- **whisper-server** - HTTP API server with OpenAI-compatible endpoints
- **whisper-quantize** - Model quantization tool
- And more...

## 📚 Documentation

For detailed usage instructions and documentation, visit:
- [whisper.cpp GitHub](https://github.com/ggml-org/whisper.cpp)
- [Official Models](https://github.com/ggml-org/whisper.cpp/blob/master/models/README.md)

## 🤝 Contributing

This repository only contains the build automation. For whisper.cpp issues or contributions, please visit the [upstream repository](https://github.com/ggml-org/whisper.cpp).

## 📝 License

The binaries are built from [whisper.cpp](https://github.com/ggml-org/whisper.cpp) which is licensed under the MIT License. See the upstream repository for details.

## ⚡ Performance Tips

### For Apple Silicon Macs (M1/M2/M3/M4)
- Use the ARM64 build with Metal GPU support
- Metal acceleration is enabled by default - no additional flags needed
- For best performance, ensure your Mac is not in low-power mode

### For Intel Macs
- Use the x86_64 build with Accelerate framework
- Consider using smaller models (tiny, base) for real-time applications
- Use the `-t` flag to specify the number of CPU threads

### General Tips
- Use quantized models (Q5_0, Q5_1) for reduced memory usage
- Enable Voice Activity Detection (VAD) for faster processing of long files
- Use smaller models for faster inference if accuracy permits

## 🐛 Issues and Support

- **Build/Release Issues**: [Open an issue here](https://github.com/bizenlabs/whisper-cpp-macos-bin/issues)
- **whisper.cpp Issues**: [Open an issue upstream](https://github.com/ggml-org/whisper.cpp/issues)

## 🙏 Acknowledgments

This project builds upon the excellent work of the [whisper.cpp](https://github.com/ggml-org/whisper.cpp) team and contributors.