# LinuxEdge

A custom embedded Linux image, hardware driver, and modern C++ gateway/agent. It works independently with a fake peripheral and becomes the bridge between CANWorks devices and SecureFleet.

## Languages

- C for kernel modules and low-level interfaces.
- C++20 for the userspace gateway and device agent.
- Shell for image and provisioning hooks.
- Device Tree Source, Kconfig, and Make for Linux integration.
- Python only for build/test helpers.

## Suggested structure

```text
linuxedge/
├── agent/                # Modern C++ service
├── board/                # Board definitions and defconfigs
├── buildroot/            # External Buildroot tree
├── drivers/              # Custom kernel driver/module
├── dts/                  # Device-tree overlays/sources
├── packages/             # Custom Buildroot packages
├── rootfs-overlay/       # systemd units and target configuration
├── scripts/
├── tests/
├── yocto/                # Later learning milestone, not initial MVP
├── .gitignore
├── ARCHITECTURE.md
└── README.md
```

## Potential libraries and packages

- Buildroot, U-Boot, and the Linux kernel
- libgpiod
- SocketCAN and `can-utils`
- fmt and spdlog
- nlohmann/json or a smaller validated serialization library
- Eclipse Paho MQTT C++ or libmosquitto
- OpenSSL or mbed TLS for transport and signature verification
- systemd `sd_notify` integration where systemd is used
- Boost.Asio or standalone Asio
- Catch2 or GoogleTest
- RAUC, SWUpdate, or Mender concepts for A/B updates; choose one only after the base image works

## Independent demonstration

Boot a minimal image, expose a Pico or simulated peripheral through a custom driver, and operate it through a supervised C++ service without any cloud dependency.

## Integration

CANWorks feeds local device data into the agent. The agent normalizes telemetry and communicates with SecureFleet. HILForge validates boot, driver, gateway, update, and rollback behavior.

