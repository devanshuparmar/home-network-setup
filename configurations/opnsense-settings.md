#!/bin/bash

# ------------------------------
# OPNsense Configuration Documentation Script
# ------------------------------
# This script documents the configuration and settings applied to
# the OPNsense firewall in a homelab setup virtualized on Proxmox.

# ------------------------------
# OPNsense VM Configuration (Proxmox)
# ------------------------------
echo "Configuring OPNsense VM settings"
# - VM Name: OPNsense Firewall
# - CPU Allocation: 2 vCPUs
# - Memory Allocation: 4 GB RAM
# - Disk Space: 16 GB virtual disk
# - Network Interfaces:
#   - LAN Interface connected to vmbr0
#   - WAN Interface connected to vmbr1

# ------------------------------
# Network Interfaces Configuration
# ------------------------------
echo "Configuring network interfaces for OPNsense"

# WAN Interface Configuration
echo "Setting up WAN interface"
# Interface Name: WAN (e.g., vtnet0)
# IP Address: 10.0.0.203 (example)
# Configuration Type: Static
# Subnet Mask: 24
# Gateway: 10.0.0.1 (example)

# LAN Interface Configuration
echo "Setting up LAN interface"
# Interface Name: LAN (e.g., vtnet1)
# IP Address: 20.0.0.1 (example)
# Configuration Type: Static
# Subnet Mask: 24
# DHCP: Enabled for 20.0.0.0/24 range (20.0.0.100-20.0.0.200)

# ------------------------------
# Firewall Rules Configuration
# ------------------------------
echo "Configuring firewall rules for OPNsense"

# WAN Rules
# - Default: Block all incoming connections unless explicitly allowed
# - Custom Rules:
#   - Allow ICMP (Ping) from trusted sources
#   - Allow outbound traffic (NAT for LAN to WAN communication)

# LAN Rules
# - Default: Allow all traffic from LAN to any destination
# - Custom Rules:
#   - Restrict traffic to certain IP ranges if needed
#   - Allow specific services (e.g., DNS, HTTP/HTTPS)

# ------------------------------
# NAT (Network Address Translation) Configuration
# ------------------------------
echo "Configuring NAT settings"
# Outbound NAT Configuration:
# - Automatic Outbound NAT: Enabled
# - Purpose: Allows traffic from LAN (20.0.0.0/24) to communicate externally via the WAN interface (10.0.0.0/24).

# ------------------------------
# DHCP Configuration
# ------------------------------
echo "Configuring DHCP for LAN interface"
# - Range: 20.0.0.100 - 20.0.0.200
# - Gateway: 20.0.0.1
# - DNS Servers: Specify if custom DNS servers are used

# ------------------------------
# VPN Configuration (if applicable)
# ------------------------------
echo "Configuring VPN settings (if applicable)"
# - IPsec / OpenVPN configuration details (if any)

# ------------------------------
# DNS Settings
# ------------------------------
echo "Configuring DNS settings"
# - DNS Forwarder/Resolver: Enabled
# - Custom DNS Servers: Specify if any

# ------------------------------
# Security Settings
# ------------------------------
echo "Configuring security settings for OPNsense"
# - Intrusion Detection/Prevention (IDS/IPS): Enabled
# - Rulesets: Specify which rulesets are used if applicable
# - Block Bogons and Private Networks: Enabled for WAN interface

# ------------------------------
# Additional Services and Plugins
# ------------------------------
echo "Configuring additional services"
# - Service 1 (e.g., Unbound DNS)
# - Service 2 (e.g., Proxy Server)

# ------------------------------
# Backup and Restore
# ------------------------------
echo "Configuring backup settings"
# - Automatic Configuration Backups: Enabled
# - Manual Backup Location: Specify location if applicable

# ------------------------------
# Troubleshooting and Future Plans
# ------------------------------
echo "Documenting troubleshooting notes and future plans"
# - Common Issues: Describe known issues and solutions
# - Connectivity Checks: Describe steps to verify network connectivity
# - Future Plans:
#   - Implement additional VLANs for network segmentation
#   - VPN enhancements for secure remote access
#   - Traffic shaping and QoS configurations

echo "OPNsense configuration documentation completed."

