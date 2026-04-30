<div align="center">

# motorbridge

**Unified motor control — one API, all vendors, every platform.**

[![Release](https://img.shields.io/github/v/release/motorbridge/motorbridge?label=release&color=brightgreen)](https://github.com/motorbridge/motorbridge/releases)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/motorbridge/motorbridge/blob/main/LICENSE)
[![PyPI](https://img.shields.io/pypi/dm/motorbridge?color=3776AB&logo=python&logoColor=white)](https://pypi.org/project/motorbridge/)

[![Rust](https://img.shields.io/badge/rust-2021-orange?logo=rust&logoColor=white)](https://www.rust-lang.org/)
[![Python](https://img.shields.io/badge/python-3.10+-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![C++](https://img.shields.io/badge/C++-RAII-00599C?logo=c%2B%2B&logoColor=white)](https://isocpp.org/)
[![ESP-IDF](https://img.shields.io/badge/ESP--IDF-5.5-E7352C?logo=espressif&logoColor=white)](https://docs.espressif.com/projects/esp-idf/en/latest/)

[![Linux](https://img.shields.io/badge/Linux-SocketCAN-FCC624?logo=linux&logoColor=black)](https://docs.kernel.org/networking/can.html)
[![macOS](https://img.shields.io/badge/macOS-PCAN-000000?logo=apple&logoColor=white)]()
[![Windows](https://img.shields.io/badge/Windows-PCAN-0078D4?logo=windows&logoColor=white)]()
[![Platform](https://img.shields.io/badge/platform-x86%20%7C%20ARM64-lightgrey)](https://github.com/motorbridge/motorbridge/releases)

</div>

---

## What We Build

A **bottom-up, fully open-source robotics platform** — from motor drivers to arm control, from embedded to cloud, from real-time control to AI agents.

- **Motor Drivers** — Plug in CAN bus and go. Damiao, RobStride, MyActuator, HighTorque, Hexfellow — one API for all.
- **Smart Servos** — Serial bus servo control with native CLI, C ABI, Python, and WASM support.
- **Embedded & MCU** — ESP32 firmware for direct motor control or wireless bridging.
- **Cross-Platform** — Linux, macOS, Windows. x86 and ARM. Rust for performance, Python for ease, C/C++ ABI for ecosystem integration.
- **ROS 2** — Native DDS bridge, no local ROS install required.
- **Robotic Arm SDK** — Full stack: connect, enable, move, calibrate, monitor.
- **Dynamics Engine** — WASM-first rigid-body dynamics: FK/IK, Jacobian, collision, trajectory planning.
- **AI Integration** — MCP server for natural language motor control via Claude, Cursor, and more.
- **Debugging & Tooling** — Web dashboard, CLI, parameter tuning, calibration workflows.

## Projects

### Core

| Project | Description |
|---|---|
| [**motorbridge**](https://github.com/motorbridge/motorbridge) | Core engine — Rust controller, C ABI, Python/C++ bindings, unified CLI |
| [**motorbridge-esp32**](https://github.com/motorbridge/motorbridge-esp32) | ESP-IDF firmware for CAN motor control & wireless bridging |
| [**motorbridge-smart-servo**](https://github.com/motorbridge/motorbridge-smart-servo) | Rust smart servo stack — CLI, C ABI, PyO3 wheels, WASM core |

### Integration

| Project | Description |
|---|---|
| [**motorbridge-ros2**](https://github.com/motorbridge/motorbridge-ros2) | Native ROS2/DDS bridge via RustDDS — no local ROS install needed |
| [**motorbridge-agent**](https://github.com/motorbridge/motorbridge-agent) | MCP server for AI-driven motor control (Claude, Cursor, etc.) |

### Products

| Project | Description |
|---|---|
| [**motorbridge-arm**](https://github.com/motorbridge/motorbridge-arm) | Serial robotic arm SDK — lifecycle, joint-space control, safety |
| [**pinocchio-wasm**](https://github.com/motorbridge/pinocchio-wasm) | WASM rigid-body dynamics — FK/IK, Jacobian, RNEA, collision |

### Tools & Docs

| Project | Description |
|---|---|
| [**motorbridge-studio**](https://github.com/motorbridge/motorbridge-studio) | Web control panel for real-time motor operation & tuning |
| [**motorbridge-docs**](https://github.com/motorbridge/motorbridge-docs) | Bilingual documentation site — API ref, tutorials, guides |

## Join Us

We welcome you to bring your motors, your robots, and your application scenarios — let's explore together.

Whether you're into embedded systems, motion planning, web tooling, or just want to drive motors — this is a bottom-up, fully open-source community, and **everyone is welcome to contribute.**

- Open an issue or PR in any of our repos
- Drop a mail: **tian.r.king@gmail.com**
- Maintainer: [@tianrking](https://github.com/tianrking)
