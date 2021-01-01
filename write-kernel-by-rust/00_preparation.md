# 环境准备

### 安装 rust
本机环境是 Ubuntu 20.04 LTS
> curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

当前 rust 版本 1.49.0，有了安装选项：
```
info: downloading installer

Welcome to Rust!

This will download and install the official compiler for the Rust
programming language, and its package manager, Cargo.

Rustup metadata and toolchains will be installed into the Rustup
home directory, located at:

  /home/zhuang/.rustup

This can be modified with the RUSTUP_HOME environment variable.

The Cargo home directory located at:

  /home/zhuang/.cargo

This can be modified with the CARGO_HOME environment variable.

The cargo, rustc, rustup and other commands will be added to
Cargo's bin directory, located at:

  /home/zhuang/.cargo/bin

This path will then be added to your PATH environment variable by
modifying the profile files located at:

  /home/zhuang/.profile
  /home/zhuang/.bashrc

You can uninstall at any time with rustup self uninstall and
these changes will be reverted.

Current installation options:


   default host triple: x86_64-unknown-linux-gnu
     default toolchain: stable (default)
               profile: default
  modify PATH variable: yes

1) Proceed with installation (default)
2) Customize installation
3) Cancel installation
```
选择1默认安装，然后验证：
> cargo --version