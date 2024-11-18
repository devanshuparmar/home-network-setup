#!/bin/bash

# ------------------------------
# OPNsense NAT and Port Forwarding Configuration Documentation
# ------------------------------
# This script provides documentation for the NAT and port forwarding configurations
# applied to the OPNsense firewall for translating traffic and enabling Plex server access.

# ------------------------------
# NAT Configuration: Translating 20.0.0.0/24 to 10.0.0.0/24
# ------------------------------
echo "Configuring NAT rules for translating 20.0.0.0/24 network to 10.0.0.0/24"

# Description:
# This NAT rule allows devices on the 20.0.0.0/24 network (internal) to communicate with
# the 10.0.0.0/24 network (external) by translating network traffic.
# Configuration Steps (Performed in OPNsense UI):
# 1. Navigate to Firewall -> NAT -> Outbound.
# 2. Select "Hybrid Outbound NAT rule generation" and click "Save".
# 3. Click "Add" to create a new rule:
#    - Interface: WAN
#    - Source Network: 20.0.0.0/24
#    - Translation Address: (Typically set to WAN address, e.g., 10.0.0.x)
#    - Description: "Translate 20.0.0.0/24 to 10.0.0.0/24"
# 4. Click "Save" and "Apply Changes".

# Note: Ensure firewall rules are configured appropriately to allow traffic as needed.

# ------------------------------
# Port Forwarding for Plex Server (Port 32400)
# ------------------------------
echo "Configuring port forwarding for Plex server (port 32400)"

# Description:
# This configuration allows incoming traffic on port 32400 to be forwarded
# to the Plex server running on the 20.0.0.0/24 network.
# Configuration Steps (Performed in OPNsense UI):
# 1. Navigate to Firewall -> NAT -> Port Forward.
# 2. Click "Add" to create a new rule:
#    - Interface: WAN
#    - Protocol: TCP
#    - Destination Address: WAN address (e.g., 10.0.0.x)
#    - Destination Port Range: 32400 (both "from" and "to" ports)
#    - Redirect Target IP: IP address of the Plex server (e.g., 20.0.0.x)
#    - Redirect Target Port: 32400
#    - Description: "Port forward for Plex server (32400)"
# 3. Click "Save" and "Apply Changes".
# 4. Ensure a corresponding firewall rule is created (if not automatically added)
#    to allow incoming traffic on port 32400.

# ------------------------------
# Verification Steps
# ------------------------------
echo "Verifying configurations"

# NAT Verification:
# - Confirm that traffic from 20.0.0.0/24 is being properly translated and can
#   communicate with 10.0.0.0/24 network devices.

# Port Forwarding Verification:
# - Test external access to the Plex server using its public IP address and port 32400.
# - Ensure the Plex server is accessible both locally and remotely.

echo "NAT and Port Forwarding configuration documentation completed."

