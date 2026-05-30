# Project Haris

> "Haris" (حارس) means guardian.

Project Haris is a maritime cybersecurity lab and platform focused on secure vessel telemetry collection, remote operations, and M-SOC infrastructure.

## What Lives Here

The repositories in this workspace map to a practical edge-to-core stack:

- Vessel-side collection on Raspberry Pi hardware
- Secure connectivity over Tailscale
- Ansible-driven deployment and hardening
- Central logging and monitoring on M-SOC nodes
- Supporting tooling for topology visibility and research

## Active Repositories

| Repository | What it does |
| --- | --- |
| [`marine_haris`](https://github.com/project-haris/marine_haris) | Edge platform for vessel data collection, Signal K integration, and Haris service deployment on Raspberry Pi systems |
| [`watchtower`](https://github.com/project-haris/watchtower) | Ansible automation for vessel-edge and M-SOC infrastructure, including hardening, Tailscale, ELK, and Zabbix deployment |
| [`haris.oversight.ee`](https://github.com/project-haris/haris.oversight.ee) | Static public site for the Haris platform |
| [`tailscale-topography`](https://github.com/project-haris/tailscale-topography) | Small local web app that visualizes Tailscale peers and tailnet topology |
| [`vsat-honeypot`](https://github.com/project-haris/vsat-honeypot) | Research honeypot that emulates a SAILOR 900 VSAT management interface for authorized lab use |

## Current Topology

From the checked-in `watchtower` inventory and playbooks, the current layout is:

- `vessel_edge`: `haris-sinilind`
- `msoc_core`: `haris-gateway`, `haris-citadel`

The current automation applies:

- `group_vessel_edge`: system prep, SSH hardening, firewalling, cron, Chrony, Zabbix agent, and the custom `haris` role
- `group_msoc_core`: shared hardening plus Tailscale, Zabbix, and optional ELK/Zabbix server services

`haris-citadel` is configured to run the ELK stack and Zabbix server, while the vessel edge host forwards logs toward the SOC side.

## Architecture

```text
Vessel network
  -> PiCAN-M / NMEA ingest
  -> Raspberry Pi edge node running marine_haris
  -> Tailscale tunnel
  -> M-SOC nodes managed by watchtower
  -> ELK and Zabbix services on haris-citadel
```

## Focus Areas

- Maritime telemetry and Signal K ingestion
- Secure vessel-to-shore connectivity
- Infrastructure-as-code for edge and M-SOC hosts
- Monitoring, logging, and operational visibility
- Defensive research around maritime-exposed systems

## Notes

- This organization contains research and operational tooling intended for authorized environments.
- Individual repositories may have different maturity levels and documentation depth as the platform evolves.

## Contact

For technical or research contact: [ahmed.nasr@oversight.ee](mailto:ahmed.nasr@oversight.ee)
