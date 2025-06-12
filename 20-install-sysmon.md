# Step 20: Install Sysmon on Windows 11

## Overview

In this step, we’ll install Sysmon (System Monitor) on your Windows 11 VM to enhance visibility into system activity. Sysmon is a powerful utility from Microsoft’s Sysinternals suite that captures detailed logging of system-level events—ideal for threat hunting, incident response, and cyber forensics.

---

## What is Sysmon?

**Sysmon** is a system service and device driver that logs detailed information about:

- Process creation and command-line arguments
- Network connections and their associated processes
- File creation time changes
- Driver and DLL loading
- Disk access with raw read operations
- Correlation with GUIDs for both sessions and processes
- Hashing of binaries (SHA1, SHA256, MD5, or IMPHASH)
- Early boot activity

It’s especially useful when paired with a SIEM or other logging/alerting platform. It runs as a **protected process**, making it resilient to tampering by most user-mode malware.

---

## Step 1: Download Sysmon

- Official download:  
  [https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)

- Download and unzip the file. You should see `Sysmon.exe`, `Sysmon64.exe`, and the EULA.

---

## Step 2: Download the Sysmon Modular Config

- Visit:  
  [https://github.com/olafhartong/sysmon-modular](https://github.com/olafhartong/sysmon-modular)

- Scroll down and download a **pre-generated config** (e.g., `config.xml`).

---

## Step 3: Prepare for Installation

1. Move the unzipped Sysmon folder to the root of the `C:` drive:
   ```
   C:\Sysmon\
   ```
2. Place the `config.xml` file inside this folder.

---

## Step 4: Install Sysmon

1. Open **Command Prompt as Administrator**.
2. Navigate to the Sysmon folder:
   ```cmd
   cd C:\Sysmon
   ```
3. Run the installation:
   ```cmd
   sysmon -accepteula -i config.xml
   ```

   If successful, you’ll see confirmation that Sysmon has been installed and is monitoring events.

---

## Step 5: Verify Installation

1. Open **Event Viewer** as Admin.
2. Navigate to:
   ```
   Applications and Services Logs > Microsoft > Windows > Sysmon > Operational
   ```
3. If events are populating here, then Sysmon is working correctly and actively logging system activity.

---

## What I Learned

- How to install a protected, persistent monitoring agent in Windows
- How Sysmon provides deep visibility into process, network, and file activity
- How to structure configuration with modular YAML/XML templates
- How to verify operational logging using Event Viewer

---

You now have high-fidelity telemetry being piped from your Windows machines like it's on a crime procedural TV show—but real, and you’re the analyst. Next up: more tools, more insights, and probably more typing.
