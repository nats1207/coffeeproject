# Homelab Starting Kit

A beginner's guide to setting up your first homelab with a Raspberry Pi.

---

## 1. Hardware

Your Raspberry Pi is the perfect starting point. No extra hardware is needed for month one.

**Recommended Pi setup (~$100–130 total):**

| Item | Recommendation |
|---|---|
| **Board** | Raspberry Pi 4 (4GB RAM is the sweet spot) |
| **microSD** | Samsung Endurance 32GB+ (built for continuous writes) |
| **Power supply** | Official Raspberry Pi USB-C supply (cheap ones cause crashes) |
| **Case** | Argon NEO (passive cooling, no fan noise) |

**Month two upgrade:** Boot from a USB SSD instead of microSD for reliability. A 256GB SSD + USB 3.0 enclosure costs ~$30 and is far more durable.

---

## 2. Operating System

Install **Raspberry Pi OS Lite (64-bit)** — no desktop, no bloat. It runs headless (no monitor needed) and teaches real Linux skills that transfer to any server.

**How to flash it:**
1. Download **Raspberry Pi Imager** from raspberrypi.com
2. Choose *Raspberry Pi OS Lite (64-bit)*
3. Before writing, click the gear icon ⚙️ and set:
   - Your hostname (e.g. `homelab`)
   - Your username and password
   - Your Wi-Fi credentials (or use ethernet — preferred)
   - **Enable SSH**
4. Flash to your microSD, insert into the Pi, power on

**Connect from your computer:**
```bash
ssh yourname@homelab.local
```

---

## 3. Networking Basics You Need to Know

- **Static IP via DHCP reservation:** Log into your router and assign your Pi a fixed local IP (e.g. `192.168.1.100`). This means the Pi's address never changes. Do this before installing anything.
- **SSH:** How you control the Pi remotely from your laptop's terminal. You already used it above.
- **Ports:** Services run on ports. Pi-hole uses port 80, Portainer uses 9000, etc. You access them via `http://192.168.1.100:9000`.
- **Tailscale (remote access):** Install this free tool to securely access your homelab from anywhere — no port forwarding into your router required.

```bash
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up
```

---

## 4. Services to Install (in order)

### Day 1 — Pi-hole (network-wide ad blocker)
Blocks ads for every device on your Wi-Fi at the DNS level. Instant "wow" factor.

```bash
curl -sSL https://install.pi-hole.net | bash
```

Then point your router's DNS to your Pi's static IP. Done.

### Day 2 — Docker + Portainer (the foundation)
Docker lets you run self-hosted apps as containers — easy to install, easy to remove, no dependency mess. Portainer gives you a web GUI to manage them.

```bash
# Install Docker
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker $USER

# Install Portainer
docker run -d -p 9000:9000 --name portainer --restart=always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v portainer_data:/data \
  portainer/portainer-ce
```

Access at `http://homelab.local:9000`

### Day 3 — Homepage + Uptime Kuma (dashboard & monitoring)
- **Homepage:** A clean dashboard showing all your services in one place.
- **Uptime Kuma:** Monitors whether your services are up and sends alerts if they go down. Both run as Docker containers via Portainer.

### Day 4 — Vaultwarden (password manager)
A self-hosted Bitwarden-compatible password manager. Your passwords, your server. Run as a Docker container.

### Month 2 — Home Assistant
Full smart-home automation platform. Controls lights, sensors, routines, and integrates with most smart-home devices. Runs well on a Pi 4 with 4GB RAM, best installed via Docker.

**RAM usage reality check (all six services):**
| Service | RAM |
|---|---|
| Pi-hole | ~80MB |
| Portainer | ~50MB |
| Homepage | ~30MB |
| Uptime Kuma | ~60MB |
| Vaultwarden | ~20MB |
| Home Assistant | ~400MB |
| **Total** | **~640MB** — fits in 4GB easily |

---

## 5. Your Action Plan

**Day 1**
- [ ] Flash Raspberry Pi OS Lite to microSD
- [ ] Boot the Pi, connect via SSH
- [ ] Set a static IP in your router
- [ ] Run system updates: `sudo apt update && sudo apt upgrade -y`

**Day 2**
- [ ] Install Pi-hole
- [ ] Point your router DNS to the Pi
- [ ] Confirm ads are being blocked on your phone

**Day 3**
- [ ] Install Docker and Portainer
- [ ] Install Tailscale for remote access

**Day 4–7**
- [ ] Add Homepage dashboard
- [ ] Add Uptime Kuma monitoring
- [ ] Add Vaultwarden

**Month 2**
- [ ] Migrate from microSD to USB SSD boot
- [ ] Set up HTTPS with a local certificate (Caddy or Nginx Proxy Manager)
- [ ] Install Home Assistant
- [ ] Explore Nextcloud (self-hosted Google Drive)

---

## Useful Resources

- [Pi-hole documentation](https://docs.pi-hole.net)
- [Tailscale quickstart](https://tailscale.com/kb/1017/install)
- [Portainer documentation](https://docs.portainer.io)
- [Home Assistant installation](https://www.home-assistant.io/installation/raspberrypi)
- [Wolfgang's Channel (YouTube)](https://www.youtube.com/@WolfgangsChannel) — excellent homelab beginner content
- [NetworkChuck (YouTube)](https://www.youtube.com/@NetworkChuck) — Pi and homelab tutorials
