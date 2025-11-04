# Cockpit Docker Manager - Debian Packaging

This repository contains Debian packaging files for [cockpit-dockermanager](https://github.com/chrisjbawden/cockpit-dockermanager).

## Overview

Cockpit Docker Manager is a lightweight Cockpit plugin for managing Docker containers through a web interface.

## Building the Package

### Quick Start

Using the provided `run` script (recommended):

```bash
# Clone the packaging repository
git clone https://github.com/hatlabs/cockpit-dockermanager-debian.git
cd cockpit-dockermanager-debian

# Clone upstream source
./run setup:clone

# Build package in Docker (no local dependencies needed)
./run package:deb:docker
```

The package will be created as `cockpit-dockermanager_*.deb` in the current directory.

### Available Commands

Run `./run help` to see all available commands:

#### Setup Commands
- `./run setup:clone` - Clone upstream cockpit-dockermanager repository
- `./run setup:pull` - Update upstream repository
- `./run setup:checkout <version>` - Checkout specific upstream version

#### Build Commands
- `./run package:deb:docker` - Build using Docker (recommended, works on any platform)
- `./run package:deb` - Build locally (requires Debian/Ubuntu with build tools)
- `./run package:docker:build` - Build/rebuild the Docker tools image

#### Core Commands
- `./run release:version` - Show current package version
- `./run help` - Show all available commands

### Building with a Specific Version

To build a specific upstream version:

```bash
./run setup:checkout v1.0.7  # or any other tag (with 'v' prefix)
echo "1.0.7" > VERSION        # Update package version (without 'v' prefix)
./run package:deb:docker
```

### Manual Build (without Docker)

If you prefer to build manually on Debian/Ubuntu:

```bash
# Install build dependencies
sudo apt-get install debhelper devscripts git

# Clone upstream source
git clone https://github.com/chrisjbawden/cockpit-dockermanager.git

# Build
dpkg-buildpackage -us -uc -b
```

## Installation

```bash
sudo dpkg -i cockpit-dockermanager_*.deb
sudo apt-get install -f  # Install any missing dependencies
```

After installation, access Cockpit at `https://your-host:9090` and find "Docker Manager" in the sidebar.

## Package Structure

- `debian/control` - Package metadata, dependencies, and debhelper compatibility level
- `debian/rules` - Build instructions
- `debian/changelog` - Version history
- `debian/copyright` - License information (machine-readable format)
- `debian/install` - File installation mappings
- `debian/source/format` - Source package format (3.0 quilt)
- `docker/` - Docker build environment for cross-platform builds
- `run` - Build automation script
- `VERSION` - Package version tracking

## Dependencies

- `cockpit` (>= 200)
- `docker.io` or `docker-ce` (recommended)

## License

The packaging files are licensed under MIT License. See [LICENSE](LICENSE) file or `debian/copyright` for full details.

The upstream software is copyright © 2025 Chris Bawden and is also MIT licensed.

## Maintainer

Matti Airas <matti.airas@hatlabs.fi>
Hat Labs
