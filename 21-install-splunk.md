# Step 21: Installing Splunk on Windows 11

## Overview

This guide walks through installing **Splunk Enterprise** on a Windows 11 VM. To avoid hitting the data ingestion limit of the free license, we’ll keep data inputs disabled by default and only enable them during testing phases.

---

## Step 1: Create a Splunk Account

- Sign up for a free Splunk trial:
  [https://www.splunk.com/en_us/download/splunk-enterprise.html](https://www.splunk.com/en_us/download/splunk-enterprise.html)

⚠️ You may need a non-personal (non-Gmail/Yahoo) email for signup.

---

## Step 2: Install Splunk

1. From your Windows 11 VM, download the `.msi` installer.
2. Accept the license agreement.
3. Run the installer and follow the prompts.
4. Choose a username and password for your Splunk instance.
5. Once installation is complete, launch Splunk.

If it doesn’t auto-open, navigate to:
```
http://localhost:8000
```

Login with the credentials you created during setup.

---

## Step 3: Install Splunk Apps

1. Click the **Apps** dropdown → **Find More Apps**
2. Search and install the following:
   - **Splunk Add-on for Sysmon**
   - **Windows Infrastructure App**

🔐 You’ll need to log in with your Splunk.com account (not your local instance login).

---

## Step 4: Configure Data Inputs

1. Go to **Settings** → **Data Inputs**
2. Select **Remote Event Log Collections**
3. Enable the collection of logs

🛑 **Important:** After testing or capturing logs, disable the data collection to avoid exceeding ingestion limits of the free license.

---

## Step 5: Quick Test

1. Open `cmd.exe`
2. Run a simple command:
   ```
   ipconfig
   ```
3. In Splunk, open the **Search & Reporting** app and search for logs related to `ipconfig`.

If everything was configured correctly, you should see at least one relevant event captured.

---

## What I Learned

- How to install and configure Splunk on a standalone VM
- The difference between Splunk accounts (cloud vs. local instance)
- How to install add-ons for data parsing and enrichment
- Managing data ingestion to avoid hitting license limits
- How to verify that logs are flowing into Splunk

---

Splunk is now up and running like a paranoid night shift guard dog. Your logs are about to be watched harder than an ex stalking on social media. Onward to more chaos and glorious insight.
