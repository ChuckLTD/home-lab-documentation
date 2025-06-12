# Step 13: Configure pfSense

## Overview

Now that pfSense is installed and running, it’s time to make it do actual firewall-y things. This includes basic setup, renaming interfaces for clarity, enabling DHCP leases, and locking down traffic between internal segments. If this feels like a lot—congrats, it is. Welcome to network engineering, lab edition.

---

## Accessing the Web Interface

1. On the Windows 11 VM, open a browser and go to `https://10.0.1.1`
2. Accept the self-signed certificate warning
3. Login using the default credentials:
   - Username: `admin`
   - Password: `pfsense`

---

## Initial Wizard Setup

Walk through the initial setup wizard. Here’s what I changed:

- Unchecked “Override DNS”  
- Changed time zone to match my local area  
- Unchecked “Block RFC1918 private networks”  
- Skipped WAN changes  
- Set a new strong admin password  
- Rebooted when prompted

---

## Renaming Interfaces

To keep things readable later, I renamed the interfaces:

- `LAN` ➝ `ECorp`
- `OPT1` ➝ `Attack LAN`

You can do this by:
- Navigating to **Interfaces > [LAN/OPT1]**
- Changing the Description field
- Saving and applying the changes

---

## DNS Resolver Tweaks

These make internal DNS resolution more efficient:

1. Go to **Services > DNS Resolver**
2. Enable:
   - DHCP Registration
   - Static DHCP
3. Under “Advanced Settings,” enable:
   - Prefetch Support
   - Prefetch DNS Key Support
4. Save and apply changes

---

## Network Performance Settings

1. Go to **System > Advanced > Networking**
2. Enable **Hardware Checksum Offloading**
3. Save and reboot if prompted

---

## DHCP Static Lease

Locking down the IP of the Windows VM to 10.0.1.2:

1. Go to **Status > DHCP Leases**
2. Find the lease for your Windows 11 VM
3. Click the "+" icon to make it static
4. Assign IP: `10.0.1.2`
5. Save and apply
6. Run `ipconfig /release` and `ipconfig /renew` from the Windows VM

---

## Creating an Alias

To simplify firewall rule creation:

1. Go to **Firewall > Aliases**
2. Create a new alias for ECorp devices
   - Type: Host(s)
   - IP: `10.0.1.2`
3. Save and apply

---

## Firewall Rules: ECorp (LAN)

Set up three rules under the **ECorp** interface:

1. **Allow Intra-ECorp traffic**
   - Source: `ECorp Alias`
   - Destination: `ECorp subnet`

2. **Allow ECorp to Attack LAN**
   - Source: `ECorp Alias`
   - Destination: `Attack LAN subnet`

3. **Allow ECorp DNS & Web**
   - Source: `ECorp Alias`
   - Destination: `any`
   - Protocols: DNS (UDP), HTTP/HTTPS

4. **Block all other traffic**
   - Source: `any`
   - Destination: `any`
   - Action: Block

Apply changes after each rule.

---

## Firewall Rules: Attack LAN

Same structure, but more strict:

1. **Allow Attack LAN to ECorp**
   - Source: `Attack LAN subnet`
   - Destination: `ECorp subnet`

2. **Block WAN access**
   - Source: `Attack LAN subnet`
   - Destination: `WAN subnet(s)`
   - Action: Block

If you ever need Kali to reach the internet, disable this rule temporarily.

---

## Final Touch: Reboot

1. Go to **Diagnostics > Reboot**
2. Choose **Normal Reboot** and hit submit

This ensures all interface changes and rules are cleanly applied.

---

## What I Learned

- The power of clean network segmentation
- How to use aliases to simplify firewall rules
- How to statically assign IPs in pfSense
- Why it’s worth naming interfaces like a sane person

Next time I say “pfSense setup,” I’ll know I actually mean “an hour of navigating cryptic tabs and remembering to click Apply.”

