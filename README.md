# HomeLab Project

My personal homelab running self-hosted services with Docker on Linux. 

# Overview:

 Host machine Lenovo thinkPad t530 (i7-3630, 8GB RAM, Intel HD 4000 + nVidia nvs 5400m, Os Linux Mint 22)

 Network devices: ISP router, 2x Mikrotik hap ax2 and tp-link archer b3600

# Network

Internet ←→ ISP Router ZTE ←→ MikroTik hAP ax2 Main  ←→  MikroTik hAP ax2 Lab  ←→ tp-link archer b3600 ←→ ThinkPad T530 - Docker Host 

ISP Router ZTE -> WAN Gateway

MikroTik hAP ax2 Main -> main router for WiFi, VPN, VLAN etc

MikroTik hAP ax2 LAB -> playground for test new service and AP for private and guest WiFi 

TP-Link archer b3600 -> AP/IoT/Smart Home idk right now

ThinkPad T530 -> Docker Host
# 

Quick Start

Prerequisites

Linux Mint 22 
Docker CE installed
Docker Compose plugin

# Install Docker 
Install dependencies
apt update && sudo apt install ca-certificates curl

# Add Docker GPG key
install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add Docker repository
 sh -c 'echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu noble stable" > /etc/apt/sources.list.d/docker.list'

# Install Docker
apt update
apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# MikroTik Configuration
Both routers run RouterOS. Configurations:

Main Router: Main router — DHCP server, firewall rules, VLAN setup

LAB Router: Access point mode — extends WiFi coverage

# Skills Demonstrated
Docker Linux MikroTik RouterOS Networking Self-hosting DNS Reverse Proxy VLANs Wi-Fi 6E

# Homelab Update — Docker, Pi-hole & MikroTik

ThinkPad T530 — Server configuration
Preventing the system from going to sleep
bash# masking sleep targets
sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target

# Config logind
sudo nano /etc/systemd/logind.conf
# Add/change:
HandleLidSwitch=ignore
HandleLidSwitchExternalPower=ignore
HandleLidSwitchDocked=ignore

sudo systemctl restart systemd-logind

ThinkPad have static IP

# Pi-hole

config:
docker-compose.yml
yamlservices:
  pihole:
    container_name: pihole
    image: pihole/pihole:latest
    network_mode: host
    environment:
      TZ: Europe/Warsaw
      WEBPASSWORD: haslo
      DNSMASQ_LISTENING: all
      PIHOLE_DNS_: 8.8.8.8;8.8.4.4
    volumes:
      - ./etc-pihole:/etc/pihole
      - ./etc-dnsmasq.d:/etc/dnsmasq.d
    restart: unless-stopped

Known limitations of Pi-hole
Pi-hole DOES NOT block:

YouTube adverts (served from the same domain as the videos)
Adverts in mobile apps (Spotify, games)
Twitch adverts

Pi-hole DOES block:

Adverts on websites
Trackers and analytics
Advert pop-ups
Most display adverts

# TODO / Następne kroki

 Nginx Proxy Manager — ładne URLe dla usług
 WireGuard VPN — po uzyskaniu publicznego IP od ISP
 Uptime Kuma — monitoring usług
 Grafana + SNMP — statystyki z MikroTika
 Vaultwarden — menedżer haseł
 Nextcloud — własny dysk w chmurze
 Wymuszone DNS przez NAT (dstnat port 53 → Pi-hole)
 
# More in future

