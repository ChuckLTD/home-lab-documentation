# Step 11: Install pfSense

## Summary

This walkthrough installs pfSense on VirtualBox. The goal is to create a virtual firewall between multiple VMs using bridged and internal networks.

## What is pfSense?

**pfSense** is an open-source firewall/router based on FreeBSD. It supports features like:
- Firewall rule sets
- NAT
- VPN (IPsec, OpenVPN)
- DHCP, DNS, VLANs

It’s commonly used in both home and enterprise networks for secure segmentation.

## Installation Steps

1. Download the pfSense Community Edition ISO  
   👉 [Download Here](https://www.pfsense.org/download/)

2. Select image type `AMD64 ISO/Virtual Machines`.

3. Extract the compressed file using 7-Zip.

4. In VirtualBox, click **New** > Name VM `pfSense`  
   - Type: BSD  
   - Version: FreeBSD (64-bit)  
   - Uncheck unattended install

5. Allocate at least:
   - **RAM**: 1024MB  
   - **CPUs**: 2  
   - **Disk**: 20GB

6. Go to VM Settings:
   - **System**: Boot Order → Uncheck Floppy, move Hard Disk to top
   - **Audio**: Disabled
   - **USB**: Disabled

## Network Adapters Configuration

- Adapter 1: **Bridged Adapter**
  - Paravirtualized Network

- Adapter 2: **Internal Network** → Name: `LAN 0`  
  - Paravirtualized Network

- Adapter 3: **Internal Network** → Name: `LAN 1`  
  - Paravirtualized Network

## pfSense Setup (Inside VM)

1. Boot and start installer.
2. Choose default options > Install pfSense CE.
3. Use Auto (UFS) for file system.
4. Reboot after install.

## pfSense Initial Configuration (Text Console)

- **No VLANs**
- Interface naming: `vtnet0`, `vtnet1`, `vtnet2`
- LAN IP: `10.0.1.1/24` with DHCP range `10.0.1.11 - 10.0.1.245`
- OPT1 IP: `10.0.3.1/24` with DHCP range `10.0.3.11 - 10.0.3.245`
- WAN: DHCP (from bridged adapter)

## Final Steps

- Remove the ISO:  
  VM Settings → Storage → Remove Disk from Virtual Drive
- Shutdown and snapshot your pfSense VM

---

🧠 **What I Learned:**
- How to bridge virtual and internal networks
- pfSense’s initial configuration via text console
- Boot sequence settings in VirtualBox are critical
