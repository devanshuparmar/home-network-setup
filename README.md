#!/bin/bash

# ------------------------------
# Homelab Network Setup Documentation
# ------------------------------
# This script-style documentation outlines the configuration, components,
# inspirations, and future plans for a custom homelab network setup.

# ------------------------------
# Overview
# ------------------------------
echo "Homelab Network Setup Overview"
# The homelab network is designed to provide a robust and secure environment for virtualization,
# network management, media streaming, and future scalability.
# Key components include:
# - Proxmox Virtualization Platform
# - OPNsense Firewall for network management and security
# - Plex Media Server containerized using Docker

# ------------------------------
# Components and Configurations
# ------------------------------

# 1. Proxmox Virtualization Platform
echo "Proxmox Virtualization Platform"
# Purpose:
# - Provides virtualization capabilities for hosting VMs and containers.
# - Hosts OPNsense for network control and Ubuntu server for Plex.
# Key Configurations:
# - VM configurations include memory allocation, vCPUs, and network bridge interfaces.
# Detailed configurations: See proxmox-settings.md

# 2. OPNsense Firewall
echo "OPNsense Firewall"
# Purpose:
# - Manages network traffic, provides security features, and enables NAT and port forwarding.
# - Handles network segmentation between external and internal interfaces.
# Key Configurations:
# - WAN and LAN interfaces for network management.
# - NAT rules for translating traffic and port forwarding for Plex.
# Detailed configurations: See opnsense-settings.md

# 3. Plex Media Server
echo "Plex Media Server"
# Purpose:
# - Provides media streaming services using Docker containers.
# - Accesses a 4TB HDD for media storage.
# Key Configurations:
# - Containerized using Docker for flexible management and scalability.
# - Port 32400 is forwarded to enable remote access.
# Detailed configurations: See plex-setup.md

# ------------------------------
# Network Structure
# ------------------------------
echo "Network Structure Overview"
# - External WAN Network (10.0.0.0/24) managed by OPNsense.
# - Internal LAN Network (20.0.0.0/24) for device communication.
# - Bridged interfaces within Proxmox for VM communication.

# ------------------------------
# Inspirations
# ------------------------------
echo "Inspirations Behind the Setup"
# This homelab project was inspired by:
# - A presentation by Ryan Mathews at BSides Saskatoon in October 2024, discussing
#   the transition to OPNsense from pfSense and running a Plex server.
# - A passion for learning and hands-on experience with advanced networking, security,
#   and virtualization concepts.

# ------------------------------
# Future Plans
# ------------------------------
echo "Future Enhancements Planned for the Homelab"
# 1. Hosting a NAS Solution
# - Centralized and efficient data storage with redundancy and sharing capabilities.

# 2. RDP (Remote Desktop Protocol) Setup
# - Secure remote access to devices within the homelab.

# 3. Access Point Configuration
# - Route physical devices through OPNsense for integration into the 100.0.0.0/24 network.

# 4. SIEM Tool Integration
# - Enhanced network security monitoring through centralized log collection and event correlation.

# ------------------------------
# Troubleshooting and Tips
# ------------------------------
echo "Troubleshooting Tips and Common Issues"
# Network Connectivity:
# - Verify NAT rules and routing configurations.
# - Ensure Plex container is running:
sudo docker ps
# Permissions:
# - Verify Plex user permissions for the 4TB HDD storage.

# ------------------------------
# Acknowledgments and Thanks
# ------------------------------
echo "Acknowledgments"
# Special thanks to the open-source community and inspirations like Ryan Mathews
# for providing insights into effective network management and media server hosting.

# ------------------------------
# License Information
# ------------------------------
echo "This project is licensed under the MIT License."
# Refer to the LICENSE file for detailed terms and conditions.

