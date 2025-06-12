# Step 18: Install Metasploitable 2

## Overview

This step walks through installing Metasploitable 2—an intentionally vulnerable virtual machine used to simulate attacks and test detection strategies within your lab network.

> **Reminder:** Metasploitable is full of vulnerabilities. Keep it isolated and never expose it to your home or production networks.

---

## Downloads

1. Download Metasploitable 2 from the [Metasploit Documentation](https://docs.rapid7.com/metasploit/metasploitable-2/).
2. Use the SourceForge link to get the `.zip` archive.
3. Extract the contents using a tool like **7-Zip**. Inside, you’ll find the `.vmdk` file used to boot the VM.

---

## Create the Virtual Machine

1. Ensure **pfSense** is running.
2. In VirtualBox, go to **Machine → New**.
3. Set:
   - **Name:** `Metasploitable2`
   - **Type:** `Linux`
   - **Version:** `Debian (64-bit)`
   - Do **not** attach an ISO image.
4. Under **Hardware**:
   - Memory: `2048 MB`
   - CPU: `1`
5. For **Hard Disk**, choose **"Do Not Add a Virtual Hard Disk"**.

---

## Add the Metasploitable VMDK

1. Go to **Settings** → **Storage**.
2. Under `Controller: SATA`, add a hard disk.
3. Select **Choose Existing Disk**, and browse to the extracted `Metasploitable.vmdk`.
4. Confirm it's listed under the controller.

---

## Final VM Settings

- **Audio:** Disable it.
- **Network Adapter 1:**
  - Set to **Internal Network**
  - Name: `LAN 1`
  - Adapter Type: **PCnet-FAST III**

> ❗ Do NOT use Paravirtualized Network (virtio-net) for Metasploitable 2.  
> It’s based on Ubuntu 8.04 and lacks the drivers for modern adapters.

- **USB:** Disable.

---

## Boot and Test

1. Start the VM.
2. Login with:
   - **Username:** `msfadmin`
   - **Password:** `msfadmin`
3. Run:
   ```bash
   ifconfig
   ```
   Confirm that the IP address is in the correct **LAN 1 subnet**, as assigned by pfSense.

---

## What I Learned

- How to safely deploy vulnerable machines in a segmented environment
- Why backward compatibility matters when selecting adapter types
- How to manually mount and use legacy virtual disk images
- Verified that Metasploitable 2 is connected to the correct subnet and reachable

---

Now your vulnerable target machine is up and running. In future steps, you’ll use this to simulate attacks, detect lateral movement, and validate the effectiveness of your defensive tools.
