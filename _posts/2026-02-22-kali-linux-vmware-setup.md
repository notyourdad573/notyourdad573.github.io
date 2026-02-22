---
title: "Making a Kali Linux VM with VMware on Windows"
date: 2026-02-22 21:00:00 -0500
categories: [Virtualization, Kali Linux]
tags: [kali, vmware, cybersecurity, virtualization, lab-setup]
---

So today we are going to set up a **Kali Linux virtual machine** using VMware on Windows and install the essential tools needed for penetration testing and lab practice.

This guide walks through everything step-by-step.

---

## Step 1 – Downloading VMware

First, open your web browser and go to:

https://access.broadcom.com/default/ui/v1/signin/

Create an account and download **VMware Workstation Player**.

After downloading:

1. Open your Downloads folder
2. Double-click the VMware installer
3. Click **Yes** if Windows asks for permission
4. Click **Next**
5. Accept the license agreement
6. Leave the default install location
7. Make sure to check:
   - Enhanced Keyboard Driver
   - Add VMware to PATH (if available)
8. Click **Install**
9. Restart your computer if prompted

---

## Step 2 – Downloading the Kali Linux Pre-Built Image

Now we’ll download Kali Linux’s pre-built VMware image.

Go to:

https://www.kali.org/get-kali/#kali-virtual-machines

Download the **VMware version**.

The file will come compressed. To extract it:

1. Download 7-Zip from:
   https://www.7-zip.org/
2. Install 7-Zip
3. Right-click the Kali file
4. Click **7-Zip → Extract Here**

This will extract the full virtual machine folder.

---

## Step 3 – Setting Up the Virtual Machine

Now open **VMware Workstation Player**.

1. Click **Open a Virtual Machine**
2. Navigate to your Downloads folder
3. Open the extracted Kali folder
4. Select the `.vmx` file inside

Before starting the VM, adjust the hardware settings:

- Set RAM to **4GB minimum**
- Set CPU cores to **2 (4 if your system allows it)**

Click **Play** to start the VM.

Default login credentials:

Username: kali 
Password: kali 

---

### If Your Mouse Does Not Show

If the mouse cursor is invisible:

1. Press **Ctrl + Alt** to release the mouse
2. Shut down the VM
3. Go to **VM → Manage → Change Hardware Compatibility**
4. Click **Next**
5. Select **Workstation 17.5 or later**
6. Finish the setup

Restart the VM and the mouse issue should be resolved.

---

## Step 4 – Installing Kali’s Tools

Once logged into Kali:

Open the Terminal (top menu or terminal icon) and run:

```bash
sudo apt update
```

Then:

```bash
sudo apt upgrade -y
```

Let this finish completely.

Now install the full Kali toolset:

```bash
sudo apt install -y kali-linux-large
```

This installs most of the commonly used penetration testing tools.

---

## Conclusion

In this guide, we:

- Installed VMware on Windows
- Downloaded Kali Linux
- Set up a working virtual machine
- Installed Kali’s toolsets

Kali Linux is a powerful operating system used for penetration testing, cybersecurity research, and ethical hacking practice.

Always make sure you have proper authorization before testing any systems.

More labs and walkthroughs coming soon.
