---
name: Beginner Homelab Pi Guide Research
description: Research and recommendations for a Pi-first beginner homelab getting-started guide — hardware, OS, services, networking, action plan
type: project
---

Researched and delivered a comprehensive Pi-first beginner homelab guide for Stan to use as source material for a getting-started YouTube tutorial or written guide.

**Why:** Target audience is complete beginners who own a Raspberry Pi but have never set it up. Goal is a practical, actionable guide with real commands and specific product recommendations.

**Key decisions and recommendations made:**

Hardware stack:
- Pi 4 4GB (~$55) or 8GB (~$75) as the sweet spot; Pi 5 8GB (~$80) if buying new
- Samsung 64GB Endurance Pro microSD as the reliable baseline
- Official USB-C power supply — non-negotiable
- Argon NEO case (~$15) for thermals
- Samsung 870 EVO 250GB SSD in USB 3.0 enclosure as the upgrade path off SD card
- APC BE425M UPS (~$40) recommended early

OS recommendation: Raspberry Pi OS Lite 64-bit (headless) via Raspberry Pi Imager — teaches real Linux skills, best community support, flexible for all services. DietPi as alternative. Home Assistant OS only if HA is the sole purpose.

Service install order (with rationale):
1. Pi-hole — DNS ad blocking, immediate visible win, teaches DNS
2. Docker + Portainer — container management UI, foundation for everything else
3. Homepage Dashboard — visual dashboard, psychological payoff
4. Uptime Kuma — monitoring and alerting, teaches observability
5. Vaultwarden — self-hosted Bitwarden, teaches "why self-host" personally
6. Home Assistant — Month 2+, needs smart home devices to shine

Networking concepts covered: static IP via DHCP reservation, DNS fundamentals, SSH, port numbers for common services, local vs remote access (Tailscale strongly recommended over port forwarding).

Tailscale is the go-to remote access recommendation — free, zero port forwarding, encrypted, works on 100 devices for personal use.

Action plan structure: Day 1 (Pi online + SSH), Day 2 (static IP + Pi-hole), Day 3-4 (Docker + Portainer), Week 2 (Tailscale), Month 2 (SSD boot, Vaultwarden with HTTPS, Home Assistant, Docker Compose, Nextcloud).

Security basics emphasized: change defaults, weekly updates, no port forwarding until understood, Tailscale over port forwarding.

3-2-1 backup rule preached from the start — SD card + external drive + cloud copy.

Community resources cited: r/homelab, r/selfhosted, awesome-selfhosted GitHub, LinuxServer.io, raspberrypi.com/documentation.

**How to apply:** Use this as the foundation for follow-up scripts, outline expansions, or deeper dives into any individual service or concept covered here.
