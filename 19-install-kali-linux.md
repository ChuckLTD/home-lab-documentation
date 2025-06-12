# Step 19: Install Kali Linux

## Overview

In this step, we'll install Kali Linux in VirtualBox and configure it to work within the internal network of your lab. Kali will serve as your offensive toolkit for red team exercises, penetration testing, and investigative learning.

---

## Download and Setup

1. Download the ISO from the official Kali website:  
   👉 [https://www.kali.org/get-kali/#kali-installer-images](https://www.kali.org/get-kali/#kali-installer-images)

2. For most Windows users: choose the **Installer Image** → **x86_64** ISO.

---

## Create the Kali VM in VirtualBox

1. In **VirtualBox**, click **New** and configure:
   - **Name:** `KaliLinux`
   - **Type:** `Linux`
   - **Version:** `Debian (64-bit)`
2. Assign:
   - **Memory:** at least `2 GB` (2048 MB)
   - **CPU:** 1–2 cores
   - **Disk size:** Minimum `20 GB`
3. Click **Finish**.

---

## Modify VM Settings

Before starting the VM:

- **System > Boot Order:** Disable Floppy; prioritize Hard Disk and Optical.
- **Audio:** Disable.
- **Network:**
  - Adapter 1 → **Internal Network**
  - Name: `LAN 1`
  - Adapter Type: **Paravirtualized Network**
- **Optional:** Disable USB if not needed.

---

## Install Kali Linux

Start the VM and:

1. Choose **Graphical Install**
2. Select:
   - Language
   - Location
   - Keyboard layout
3. Hostname: Choose one for your Kali VM
4. Leave domain name blank
5. Create a user and password
6. Select time zone
7. Choose to use the **entire disk**
8. Accept partitioning and select default values
9. Confirm installation

---

## First Boot and Network Test

After installation:

- Log in with the credentials you created
- Open Terminal and run:
  ```bash
  ip a
  ```
  Confirm you received an IP address in the correct internal network range (e.g., `10.0.1.x`).

---

## Install VirtualBox Guest Additions

1. Go to **Devices → Insert Guest Additions CD Image**
2. Open Terminal in Kali and run the following:

```bash
sudo mkdir /mnt/cdrom
sudo mount /dev/cdrom /mnt/cdrom
cd /mnt/cdrom
sudo ./VBoxLinuxAdditions.run
```

### What each command does:
- `mkdir`: Creates a mount point for the CD.
- `mount`: Mounts the virtual Guest Additions CD.
- `cd`: Enters the mounted directory.
- `VBoxLinuxAdditions.run`: Executes the installer script.

3. After installation, **reboot the system**.

You may now be able to use full-screen mode, clipboard sharing, and drag-and-drop functionality.

---

## What I Learned

- How to install and configure Kali Linux in a virtualized lab setting
- How to assign internal network settings for segmented testing
- Basic command line for verifying connectivity and installing guest tools
- Best practices for isolating offensive tools from production environments

---

Once Kali is up and running, you’re now equipped to go full Mr. Robot. Next stop: attacks, alerts, detections, and celebratory ramen noodles.
