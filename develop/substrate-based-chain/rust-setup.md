---
description: >-
  Read on to learn the steps needed to prepare a computer for development with
  the Substrate Node Template.
---

# Rust setup

Since Substrate is built with [the Rust programming language](https://www.rust-lang.org/), the first thing you will need to do is prepare the computer for Rust development. Тhe steps you take will vary based on the computer's operating system. 

Once Rust is configured, you will use its toolchains to interact with Rust projects; the commands for Rust's toolchains will be the same for all supported, Unix-based operating systems.

## Unix-based operating systems

Substrate development is easiest on Unix-based operating systems like macOS or Linux. The examples in the Substrate [Tutorials](https://substrate.dev/tutorials) and [Recipes](https://substrate.dev/recipes/) use Unix-style terminals to demonstrate how to interact with Substrate from the command line.

### macOS

Open the terminal application and execute the following commands:

```text
# Install Homebrew if necessary https://brew.sh/
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

# Make sure Homebrew is up-to-date, install openssl and cmake
brew update
brew install openssl cmake
```

### Ubuntu/Debian

Use a terminal shell to execute the following commands:

```text
sudo apt update
# May prompt for location information
sudo apt install -y cmake pkg-config libssl-dev git build-essential clang libclang-dev curl
```

### Arch Linux

Run these commands from a terminal:

```text
pacman -Syu --needed --noconfirm cmake gcc openssl-1.0 pkgconf git clang
export OPENSSL_LIB_DIR="/usr/lib/openssl-1.0"
export OPENSSL_INCLUDE_DIR="/usr/include/openssl-1.0"
```

### Fedora/RHEL/CentOS

Use a terminal to run the following commands:

```text
# Update
sudo dnf update
# Install packages
sudo dnf install cmake pkgconfig rocksdb rocksdb-devel llvm git libcurl libcurl-devel curl-devel clang
```

## Rust developer environment

This project uses [`rustup`](https://rustup.rs/) to help manage the Rust toolchain. First install and configure `rustup`:

```text
# Install
curl https://sh.rustup.rs -sSf | sh
# Configure
source ~/.cargo/env
```

Finally, configure the Rust toolchain:

```text
rustup default stable
rustup update nightly
rustup update stable
rustup target add wasm32-unknown-unknown --toolchain nightly
```

