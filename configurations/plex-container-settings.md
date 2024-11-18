#!/bin/bash

# ------------------------------
# Plex Media Server Setup and Configuration
# ------------------------------
# This script documents the steps for setting up Plex Media Server 
# Using Docker on a homelab environment with Ubuntu Server.
# NOTE: This setup assumes a fresh Ubuntu Server installation 
# with no additional settings changed.

# ------------------------------
# Prerequisites Check
# ------------------------------
echo "Checking prerequisites for Plex setup"
# Ensure Docker is installed
docker --version || { echo "Docker is not installed. Please install Docker and re-run this script."; exit 1; }
# Optional: Check for Docker-Compose if needed
docker-compose --version || echo "Docker Compose is not installed (optional but recommended for complex setups)."

# ------------------------------
# Step 1: Create a Plex User
# ------------------------------
echo "Creating Plex user (if not already created)"
# Create user and set permissions
sudo useradd -r -s /usr/sbin/nologin plex
sudo chown -R plex:plex /mnt/wd-4tb
sudo chmod -R 755 /mnt/wd-4tb

# ------------------------------
# Step 2: Prepare Directories for Plex
# ------------------------------
echo "Preparing directories for Plex configuration and transcode data"
# Create necessary directories
mkdir -p ~/plex/config
mkdir -p ~/plex/transcode
sudo chown -R plex:plex ~/plex

# ------------------------------
# Step 3: Pull the Plex Docker Image
# ------------------------------
echo "Pulling the Plex Docker image"
sudo docker pull linuxserver/plex

# ------------------------------
# Step 4: Run the Plex Docker Container (with Port 32400 Mapping)
# ------------------------------
echo "Running the Plex Docker container with port 32400 mapping"
# Replace <YOUR_PLEX_CLAIM_TOKEN> and <YOUR_SERVER_IP> with actual values
sudo docker run -d \
  --name=plex \
  --user=plex:plex \
  --network=host \
  -e PLEX_CLAIM="<YOUR_PLEX_CLAIM_TOKEN>" \
  -e ADVERTISE_IP="http://<YOUR_SERVER_IP>:32400/" \
  -p 32400:32400/tcp \  # Explicitly map port 32400 for Plex
  -v ~/plex/config:/config \
  -v ~/plex/transcode:/transcode \
  -v /mnt/wd-4tb:/media \
  --restart unless-stopped \
  linuxserver/plex

# Explanation of added options:
# --name=plex: Names the container "plex"
# --user=plex:plex: Runs the container as the "plex" user
# --network=host: Uses host network for simplicity
# -e PLEX_CLAIM="<YOUR_PLEX_CLAIM_TOKEN>": Replace with your Plex claim token
# -e ADVERTISE_IP="http://<YOUR_SERVER_IP>:32400/": Sets advertised IP for remote access
# -p 32400:32400/tcp: Maps port 32400 on the host to port 32400 on the container
# -v ~/plex/config:/config: Mounts the configuration directory
# -v ~/plex/transcode:/transcode: Mounts the transcode directory
# -v /mnt/wd-4tb:/media: Mounts the 4TB HDD for media storage
# --restart unless-stopped: Ensures the container restarts unless manually stopped

# ------------------------------
# Step 5: Access Plex for Configuration
# ------------------------------
echo "Access Plex Media Server via a web browser"
# URL for Plex Web Interface
echo "Visit http://<YOUR_SERVER_IP>:32400/web to configure your Plex Server"

# ------------------------------
# Port Forwarding for Remote Access
# ------------------------------
echo "Ensure port forwarding is configured on OPNsense"
# - Forward port 32400 to allow remote access to Plex
# Refer to opnsense-settings.md for detailed configurations.

# ------------------------------
# Troubleshooting Tips
# ------------------------------
echo "Common troubleshooting tips"
# Permission Issues:
sudo chown -R plex:plex /mnt/wd-4tb
sudo chmod -R 755 /mnt/wd-4tb

# Network Configuration:
# Verify Docker container status
sudo docker ps
# Test access to Plex
echo "Test access via http://<YOUR_SERVER_IP>:32400"

# ------------------------------
# Additional Configuration Options (Optional)
# ------------------------------
# - Custom transcoding settings based on hardware capabilities
# - Backup configuration directory for preservation

echo "Plex Media Server setup completed."

