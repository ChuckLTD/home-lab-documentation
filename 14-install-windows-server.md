# Step 14: Install Windows Server

## Overview

In this step, I set up a Windows Server 2025 VM that will later become a Domain Controller. This lays the groundwork for building out Active Directory and other enterprise services in the lab.

---

## Downloading Windows Server 2025 ISO

To start, I downloaded the free evaluation ISO of Windows Server 2025:

[Windows Server 2025 Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2025)

Yes, you have to register with Microsoft. No, there’s no way around it unless you know a wizard.

---

## Creating the VM in VirtualBox

In VirtualBox:

- Selected “New” and pointed to the Windows Server ISO
- Named the VM and verified it was recognized as a Windows environment
- Allocated memory and CPU cores (balanced with other lab VMs in mind)
- Set EFI to enabled (required for Server 2025)
- Ensured boot order prioritizes the virtual hard disk
- Disabled audio because… it’s a server

**Networking:**

- Adapter 1: Internal Network (LAN 0)
- Adapter Type: Intel PRO/1000 MT Server

---

## Installing Windows Server

1. Started the VM and hit any key when prompted (timing is crucial)
2. Chose English (language and keyboard)
3. Selected "Standard Evaluation (Desktop Experience)" as the edition
4. Accepted license agreement
5. Chose “Custom: Install Windows Only”
6. Let installation run (restarts several times)
7. Set a secure password for the local Administrator account
8. Logged in using VirtualBox’s “Insert Ctrl+Alt+Del” option

---

## Installing Guest Additions

To improve performance and integration:

- Mounted the Guest Additions ISO
- Ran VBoxWindowsAdditions-amd64.exe
- Chose default settings
- Rebooted the VM
- Resized the window to trigger full-screen mode
- Enabled clipboard sharing: Settings → General → Advanced → Shared Clipboard → Bidirectional

---

## Verifying Network Connectivity

Inside the VM, I opened a Command Prompt and ran:

ipconfig

The server picked up an IP in the expected subnet from pfSense’s DHCP.

---

## Assigning a Static IP via pfSense

To keep the IP address fixed:

1. Logged into pfSense: https://10.0.1.1
2. Went to Status > DHCP Leases
3. Found the server lease and clicked the "+" icon
4. Assigned: 10.0.1.3
5. Saved and applied the change

Then inside the server, I ran:

ipconfig /release  
ipconfig /renew

Confirmed it picked up the static lease for 10.0.1.3.

---

## What I Learned

- How to configure a Windows Server VM from scratch
- The importance of Guest Additions in usability
- How to assign static leases via pfSense
- That Ctrl+Alt+Del inside VirtualBox is… weirdly dramatic

This machine is now ready to be promoted to a Domain Controller in upcoming steps.
