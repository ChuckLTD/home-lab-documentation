# Step 16: Setting Up Users, Groups, and Policies

## Overview

This step covers the setup of user accounts, service accounts, groups, a file share, a service principal name (SPN), and a Group Policy Object (GPO) to disable Windows Defender in the lab environment.

---

## Create Organizational Unit for Groups

1. Open **Active Directory Users and Computers** from **Tools** in Server Manager.
2. Expand the domain (e.g., `ECorp.local`).
3. Right-click the domain → **New** → **Organizational Unit**.
4. Name it: `Groups`.

Move all existing groups from the **Users** container into the new **Groups** OU.

---

## Create User Accounts

1. In the **Users** folder, right-click the default **Administrator** account and select **Copy**.
2. Fill in fields to create a new admin account (e.g., `admin.lab`) and set a strong password.
3. Repeat the process to create a service account (e.g., `SQLService`).
   - Use password: `MYpassword123#`
   - Set password to never expire.

Optional: Add the password into the account's description or notes field for lab convenience (do not do this in production).

4. Create standard user accounts (e.g., `john.doe`, `jane.smith`), checking the "Password never expires" option for each.

---

## Set Up a File Share

1. In Server Manager, go to **File and Storage Services** → **Shares**.
2. Click **Tasks** → **New Share**.
3. Select default options until prompted to name the share (e.g., `SharedDocs`).
4. Accept all other defaults and click **Create**.

---

## Register a Service Principal Name (SPN)

In an elevated Command Prompt, run:

```bash
setspn -a ECorp/SQLService.ECORP.local:60111 ECORP\SQLService
```

Confirm registration:

```bash
setspn -T ECORP.local -Q */*
```

You should see your newly registered SPN in the output.

---

## Create Group Policy to Disable Windows Defender

1. Open **Group Policy Management**.
2. Expand **Forest** → **Domains** → right-click your domain (e.g., `ECorp.local`).
3. Choose **Create a GPO in this domain and link it here**.
4. Name it: `Disable Windows Defender`.

To edit the GPO:

1. Right-click the new GPO → **Edit**.
2. Navigate to:
   ```
   Computer Configuration →
   Policies →
   Administrative Templates →
   Windows Components →
   Microsoft Defender Antivirus
   ```
3. Open **Turn off Microsoft Defender Antivirus**, set it to **Enabled**, then click **OK**.

Enforce the GPO by right-clicking it and selecting **Enforced**.

---

## What I Learned

- How to create and manage users, service accounts, and organizational units
- Created a file share via Server Manager
- Registered and confirmed a Service Principal Name (SPN) for the SQL service account
- Created and enforced a Group Policy to disable Microsoft Defender
- Laid the foundation for domain policy management and domain-joined systems

---

In the next step, I’ll be joining Windows VMs to the domain to test authentication and apply GPOs.
