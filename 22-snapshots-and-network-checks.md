# Step 22: Snapshots, Snapshots, Snapshots

## Introduction

**Snapshots in VirtualBox** are saved states of a virtual machine (VM) at a specific point in time. They allow you to preserve the entire system state—including disk, memory, and VM settings—so you can revert back to it anytime.

---

### 💡 Why Snapshots Matter:

- **Testing & Experimentation:** Try changes, updates, or malware without risk. Revert if it goes sideways.
- **Safe Rollbacks:** Break something during setup? Return to a known-good state with a click.
- **Time-Saving:** Skip troubleshooting or rebuilding VMs. Restore and move on.

---

## Network Check Pre-Snapshot

Before taking snapshots, confirm that the network is working across your environment.

### ✅ Checklist:

1. **Ensure All VMs Are Running**
   - pfSense
   - Windows 11
   - Domain Controller
   - Metasploitable 2
   - Kali Linux

2. **Windows 11 Firewall**
   - Open **Firewall & Network Protection**
   - Select **Domain Network**
   - Disable **Microsoft Defender Firewall**
   - Authenticate with Domain Admin credentials

3. **Ping Test from Kali:**
   - Ping Windows 11 (`10.0.1.2`)
   - Ping Domain Controller (`10.0.1.3`)
   - Ping Metasploitable 2 (`10.0.1.13`)

All pings should be successful. If not, troubleshoot before proceeding.

---

## Taking Snapshots in VirtualBox

### Steps:

1. In **VirtualBox Manager**, select your VM (e.g., pfSense)
2. Click the **hamburger menu** (≡) and choose **Snapshots**
3. Click **Take**
4. Name your snapshot something meaningful, like:
   ```
   Pre-Attack Lab Baseline
   ```

5. Repeat this process for:
   - Windows 11 VM
   - Domain Controller
   - Metasploitable 2
   - Kali Linux

---

## Best Practices for Snapshot Naming

| Name Example                 | Description                                 |
|-----------------------------|---------------------------------------------|
| `BaseInstall-Kali`          | Right after installing Kali, pre-config     |
| `Post-Sysmon-Install`       | After setting up Sysmon                     |
| `ReadyForCTF-Windows`       | When Windows 11 is configured for testing   |
| `Metasploitable-CleanState` | Before launching scans or exploits          |

---

## What I Learned

- How to validate a functional, routable lab environment
- How to use VirtualBox snapshots effectively
- Why snapshot management is essential in cybersecurity labs

---

Congrats! Your cyber range is now preserved in stasis like a digital time capsule. Now you can break, pwn, or hack to your heart’s content—just don't forget to snap back when you're done.
