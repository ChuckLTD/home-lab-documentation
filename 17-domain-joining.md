# Step 17: Domain Joining

## Overview

This walkthrough covers the process of joining your Windows 11 VMs to the domain you previously created, confirming successful integration, and connecting to a domain-based network share.

---

## Set Static IP for Windows VM

1. Open **Network & Internet Settings**.
2. Go to **Ethernet** → **Edit IP Assignment**.
3. Set IP to **Manual**:
   - IP Address: `10.0.1.2`
   - Subnet: `255.255.255.0`
   - Gateway: `10.0.1.1` (router)
   - Preferred DNS: `10.0.1.3` (domain controller)

Save changes.

---

## Join the Domain

1. Open **Access Work or School** from the Start menu.
2. Select **Connect** → **Join this device to a local Active Directory domain**.
3. Enter your domain name (e.g., `ECORP.local`) and click **Next**.
4. Enter domain admin credentials.
5. Set account type to **Administrator** when prompted.
6. Restart the VM.

---

## Confirm the Join

1. Log in to your domain controller.
2. Open **Active Directory Users and Computers**.
3. Expand the **Computers** container—you should see the newly joined VM listed.

Success! 🎉 Your machine is now part of the domain.

---

## Optional: Connect to Network Share

1. On the domain-joined VM, log in using a domain account:
   - Format: `ECORP\username`
2. On first login, Windows will take time to configure the profile.
3. Open **User Account Settings** to confirm group membership if needed.
4. Add a domain user to the **Local Administrators** group (if required).
5. Open File Explorer → **Network**.
6. Locate your domain controller and double-click it.
7. Log in if prompted.
8. You should now see and be able to access the network share created in previous steps.

Repeat the domain join process for any additional Windows VMs in your lab.

---

## What I Learned

- How to configure a static IP and DNS to align with lab subnet
- How to join a Windows machine to an Active Directory domain
- How to access domain-based resources like network shares
- Validated successful join through Active Directory and file share connectivity

---

Next up: configuring more tools and beginning lab-based detection and attack simulations. This is where the real fun begins.
