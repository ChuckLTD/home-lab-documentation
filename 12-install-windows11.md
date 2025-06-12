# Step 12: Install Windows 11 VM

## Summary

This step covers installing a Windows 11 virtual machine in VirtualBox for use inside the home lab. I’m using the Windows 11 Enterprise ISO provided by Microsoft’s Evaluation Center—free for 90 days. This machine will eventually be domain-joined, monitored by Sysmon, and used to simulate attacks and policies.

---

## Downloading Windows 11

You can grab the ISO directly from Microsoft here:  
🔗 [Windows 11 Enterprise | Microsoft Evaluation Center](https://www.microsoft.com/en-us/evalcenter/download-windows-11-enterprise)

You’ll need to register and choose your language. Select the **64-bit** version and save it somewhere easy to find.

---

## Creating the VM in VirtualBox

Once the ISO is downloaded:

1. **Open VirtualBox** and click **New**
2. Name the VM something like `Win11-Lab`
3. Under ISO Image, browse to the ISO you downloaded
4. The OS type/version should autofill to Windows 11, but confirm it's correct
5. **Skip unattended installation** (this is important)
6. Allocate hardware:
   - 2 CPUs  
   - 4GB+ RAM (based on your system)
   - Enable EFI (required for Win11 install to work properly)
7. Create a virtual hard disk:
   - 50GB recommended
   - Dynamically allocated (don’t pre-allocate full size)

---

## VM Settings Tweaks (Important!)

Before launching the install, update the following:

- **System → Boot Order:**
  - Move Hard Disk to the top
  - Uncheck Floppy
  - Re-enable EFI and Secure Boot afterward

- **Audio → Disable**

- **Network → Adapter 1:**
  - Set to **Internal Network**
  - Name: `LAN 0`
  - Adapter Type: **Intel PRO/1000 MT Desktop**

This adapter will let the VM get its IP from pfSense via DHCP.

---

## Installing Windows 11

Start the VM and be ready to hit a key when prompted—if you miss the window, you’ll have to reboot. Trust me, I missed it once.

- Choose your language, region, and keyboard
- Accept license terms and click **Next**
- Start the full installation (no product key required for the evaluation)
- Select **Domain Join instead** when asked for a Microsoft account
- Create a local user and password (don’t forget this!)
- Skip second keyboard and unnecessary settings
- After updates and restarts, log in with your local account

---

## Test Network Connectivity

After logging in:

1. Open **Command Prompt**
2. Run `ipconfig`

You should see a 10.0.1.x IP if DHCP is working and pfSense is configured properly.

---

## Optional: Install Guest Additions

To make your life easier, install VirtualBox Guest Additions:
- Mount the ISO (Devices > Insert Guest Additions CD Image)
- Run the installer and reboot
- Enable clipboard sharing (Settings > General > Advanced → Bidirectional)

This gives you:
- Better graphics/resolution
- Shared clipboard
- Drag-and-drop (sometimes)

---

## What I Learned

- How to configure VM hardware for Windows 11 (EFI and Secure Boot are non-negotiable)
- Bridging the VM to an internal virtual network
- DHCP and IP testing through pfSense
- How to create a usable, snapshot-ready lab endpoint

