# Marine Haris

> **"Haris"** (حارس) - Arabic for "Guardian" or "Protector"

Maritime Security Operations Center (MSOC) infrastructure for secure vessel data collection and transmission.

## Overview

Marine Haris provides an open-source platform for maritime security operations, enabling real-time monitoring and data collection from vessels to onshore security operations centers.

## Projects

| Repository | Description |
|------------|-------------|
| [Marine_Haris](https://github.com/marineharis/Marine_Haris) | Edge device software for vessel data collection (NMEA 2000/0183, Signal K) |
| [Watchtower](https://github.com/marineharis/Watchtower) | Ansible automation for deploying and managing edge devices and MSOC infrastructure |

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         VESSEL LAYER                            │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────────────┐  │
│  │ NMEA Network│───▶│ PiCAN-M HAT │───▶│ Raspberry Pi 5      │  │
│  │ (2000/0183) │    │             │    │ Marine_Haris Edge   │  │
│  └─────────────┘    └─────────────┘    └──────────┬──────────┘  │
│                                                   │             │
│                                         ┌────────▼────────┐     │
│                                         │  Tailscale VPN  │     │
│                                         └────────┬────────┘     │
└──────────────────────────────────────────────────┼──────────────┘
                                                   │
                                                   │ Encrypted
                                                   │ Tunnel
                                                   │
┌──────────────────────────────────────────────────┼──────────────┐
│                         MSOC LAYER               ▼              │
│  ┌─────────────────┐    ┌─────────────────────────────────┐     │
│  │  Haris Gateway  │◀───│       ELK Stack / Logs          │     │
│  └────────┬────────┘    └─────────────────────────────────┘     │
│           │                                                     │
│           ▼                                                     │
│  ┌─────────────────┐                                            │
│  │ Haris Citadel   │  Central monitoring & analysis             │
│  └─────────────────┘                                            │
└─────────────────────────────────────────────────────────────────┘
```

## Key Features

- **NMEA Data Collection**: Parse and process NMEA 2000 and NMEA 0183 vessel data
- **Signal K Integration**: Open marine data standard support
- **Secure Transmission**: WireGuard/Tailscale encrypted VPN tunnels
- **Edge Computing**: Real-time processing on Raspberry Pi hardware
- **Centralized Logging**: ELK stack for log aggregation and analysis
- **Infrastructure as Code**: Ansible-based deployment automation

## Quick Links

- [Marine_Haris Documentation](https://github.com/marineharis/Marine_Haris#readme)
- [Watchtower Deployment Guide](https://github.com/marineharis/Watchtower#readme)

## Hardware

| Component | Purpose |
|-----------|---------|
| Raspberry Pi 5 (16GB) | Edge processing unit |
| PiCAN-M HAT | Marine CAN bus connectivity |
| NVMe SSD (128GB) | Local storage |
| TP-Link Archer NX200 | Cellular connectivity |

## Security

- End-to-end encryption via Tailscale (WireGuard)
- Tamper-evident hardware design
- Secure boot with storage encryption
- Network isolation with firewall rules

## License

MIT License - see individual repositories for details.

## Contact

For technical support or security concerns: marineharis@ahmdngi.io

---

**Notice**: This system is for authorized maritime security operations only.
