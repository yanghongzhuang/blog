# 环境准备

本机环境是 Ubuntu 20.04

#### 安装 qemu
```
sudo apt install qemu-system-x86
```

#### 安装 nasm
```
sudo apt install nasm
```

#### 安装 rust
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

#### 验证
```
> qemu-system-i386 --version
QEMU emulator version 4.2.1 (Debian 1:4.2-3ubuntu6.10)
Copyright (c) 2003-2019 Fabrice Bellard and the QEMU Project developers

> nasm -v
NASM version 2.14.02

> rustc --version
rustc 1.49.0 (e1884a8e3 2020-12-29)
```
