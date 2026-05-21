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

# More in future

