# build-ladybird-macos

Pre-built [Ladybird](https://ladybird.org) browser binaries for **macOS ARM64** (Apple Silicon M1/M2/M3/M4).

Built **daily** via GitHub Actions — grab the latest `.tar.gz` from the [releases page](https://github.com/mrndstvndv/build-ladybird-macos/releases/tag/nightly) or from the [Actions tab](https://github.com/mrndstvndv/build-ladybird-macos/actions).

## Usage

1. Download the latest `Ladybird-macOS-ARM64.tar.gz` from [Releases](https://github.com/mrndstvndv/build-ladybird-macos/releases/tag/nightly).
2. Extract:
   ```bash
   tar xzf Ladybird-macOS-ARM64.tar.gz
   ```
3. Drag `Ladybird.app` to your **Applications** folder, or run directly:
   ```bash
   open Ladybird.app
   ```

> **Note:** Ladybird is pre-alpha software. Expect missing features, crashes, and incomplete web compatibility.

## Why?

Building Ladybird from source takes **40–90 minutes** and requires LLVM 21, CMake, Ninja, vcpkg fetching/builds all C++ dependencies (OpenSSL, ICU, Skia, etc.), and a C++23 toolchain. This repo does that work once so you don't have to.

## How it works

A scheduled GitHub Actions workflow (`macos-15` runner, Apple Silicon):
1. Clones `LadybirdBrowser/ladybird`
2. Installs Homebrew deps (LLVM 21, CMake, Ninja, etc.)
3. Runs `Meta/ladybird.py build` with Homebrew Clang
4. Caches `ccache` and `vcpkg` binary cache across runs for incremental rebuilds
5. Packages `Ladybird.app` as a `.tar.gz`
6. Publishes to the **nightly** release

## License

Ladybird is BSD-2-Clause licensed. The source is at [LadybirdBrowser/ladybird](https://github.com/LadybirdBrowser/ladybird).
