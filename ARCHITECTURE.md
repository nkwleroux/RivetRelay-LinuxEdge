# LinuxEdge Architecture

## Layers

```text
U-Boot -> Linux kernel/device tree -> custom driver -> userspace agent
       -> local persistence/buffering -> MQTT or HTTPS -> SecureFleet
```

## Process boundaries

- Kernel code exposes hardware through a narrow stable userspace API.
- The agent owns protocol translation, configuration, buffering, health, and cloud transport.
- Update logic is separated from application logic and must verify signatures before activation.
- A fake-driver adapter allows the agent to run on desktop Linux.

## Failure behavior

The gateway must tolerate missing CAN nodes, cloud outages, corrupted local configuration, agent crashes, interrupted updates, and unsuccessful post-boot health checks.

