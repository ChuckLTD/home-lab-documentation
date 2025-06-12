# Step 15: Install and Configure Active Directory

## Overview

In this step, I installed Active Directory Domain Services on my Windows Server VM, promoted it to a Domain Controller, added Certificate Services, and configured network settings. This sets the stage for centralized identity management in the home lab.

---

## Rename the Server

1. Open the Start menu and type “name”.
2. Select “Rename this PC”.
3. Enter a meaningful hostname for your Domain Controller (e.g., `DC01`) and restart the server.

---

## Install Active Directory Domain Services

1. Open **Server Manager** → select **Manage** → **Add Roles and Features**.
2. Click **Next** until you reach the **Server Roles** section.
3. Select **Active Directory Domain Services**.
4. Click **Add Features** when prompted.
5. Continue clicking **Next** until you reach the confirmation page.
6. Enable the “Restart if required” checkbox and then click **Install**.
7. Wait for installation to complete.

---

## Promote to Domain Controller

1. After installation, click “Promote this server to a domain controller”.
2. Choose **Add a new forest** and provide a **root domain name** (e.g., `ecorp.local`).
3. Set a **Directory Services Restore Mode (DSRM)** password.
4. Accept the default NetBIOS name when it auto-populates.
5. Click **Next** through remaining steps until you reach **Prerequisites Check**.
6. Once it passes, click **Install**. The server will restart after promotion.

---

## Install Active Directory Certificate Services (AD CS)

1. After reboot, log back into the server.
2. Open **Server Manager** → **Manage** → **Add Roles and Features**.
3. Click **Next** to the **Server Roles** page.
4. Select **Active Directory Certificate Services**.
5. Click **Add Features** when prompted.
6. Continue clicking **Next** and enable **Restart if required**.
7. Click **Install**.

---

## Configure AD CS

1. Once installed, select **Configure Active Directory Certificate Services**.
2. On the setup wizard:
   - Choose the local server.
   - Select **Certificate Authority** role.
   - Choose **Enterprise CA**.
   - Select **Root CA**.
   - Choose **Create a new private key**.
   - Leave default cryptographic options (RSA 2048 / SHA256).
   - Accept default certificate name and validity period.
   - Accept the default database locations.
3. Click **Configure** to complete setup.
4. When you receive “Configuration succeeded”, restart the server.

---

## Set Static Network Information

1. Open **Network & Internet settings** from the system tray.
2. Select the **Ethernet** connection.
3. Click **Edit IP assignment** and switch to **Manual / IPv4**.
4. Set:
   - IP: `10.0.1.3`
   - Subnet: `255.255.255.0`
   - Gateway: `10.0.1.1`
   - DNS: `10.0.1.3`
5. Save the configuration.
6. Open Command Prompt and run:

```bash
ipconfig /all
```

7. Confirm the IP, Gateway, and DNS match your domain controller setup.

---

## What I Learned

- How to install and configure AD DS and promote a Windows Server to Domain Controller
- Installed and configured AD CS for future certificate issuance
- Set static IP and verified DNS alignment
- Got a solid grasp on how Windows networking ties into domain infrastructure

The Domain Controller is now ready to manage users, groups, and policies in upcoming steps.
