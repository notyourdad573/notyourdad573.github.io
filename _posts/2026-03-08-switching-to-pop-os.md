---
title: "Switching From Windows to Pop!_OS (My Step-by-Step Setup)"
date: 2026-03-08
categories: [Linux, Homelab]
tags: [linux, pop-os, cybersecurity, homelab]
---

# Switching From Windows to Pop!_OS (My Step-by-Step Setup)

So I recently decided to switch my main desktop from Windows over to **Pop!_OS**, and honestly it was way smoother than I expected. I’m still learning Linux, but I’ve been messing around with Kali and lab environments for a bit, so I figured it was time to make the jump on my main machine.

If you’re thinking about doing the same thing, here’s the exact process I used to move from Windows to Pop!_OS.

---

## Step 1 — Back Up Your Important Stuff

Before you do anything, back up your important files. When you install Linux and choose a clean install, it **will wipe your drives**.

Things I recommend backing up:

- Documents
- Pictures
- Password exports or browser sync
- Game saves if you care about them
- Any project files

I personally made sure my browser was synced and copied anything important to another drive.

---

## Step 2 — Download Pop!_OS (Important if you have older NVIDIA GPUs)

Go to the official Pop!_OS website and download the installer.

You’ll see different installer options depending on your hardware.

Normally you would choose:

- **NVIDIA version** – if you have an NVIDIA GPU  
- **Intel/AMD version** – if you don’t

However I ran into an issue because I’m using a **GTX 1080 Ti**.

The newest installer build didn’t play nicely with my GPU, so instead I installed:

**Pop!_OS 24.04 LTS**

Details for the version I used:

- File Size: 2.91 GB
- Requirements:
  - 4 GB RAM
  - 16 GB storage
  - 64-bit processor

This version is recommended for systems with:

- Intel graphics
- AMD graphics
- **NVIDIA 10-series GPUs and older (like the GTX 1080 Ti)**

So if you’re running similar hardware and the newest installer gives you issues, grabbing the **24.04 LTS ISO** worked perfectly for me.

---

## Step 3 — Make a Bootable USB

You’ll need a USB drive (8GB or bigger).

I used **Balena Etcher** to flash the installer.

Steps:

1. Plug in your USB drive
2. Open Balena Etcher
3. Select the Pop!_OS ISO file
4. Select your USB drive
5. Click **Flash**

After that finishes you’ll have a bootable Pop!_OS installer.

---

## Step 4 — Enter Your BIOS

Restart your computer and open the BIOS.

The key depends on your motherboard, but common ones are:

- F2
- F12
- DEL
- ESC

Once you're in the BIOS there are two things you should check.

Disable:

```
Secure Boot
```

Then make sure your USB drive is first in the boot order.

---

## Step 5 — Boot Into the Pop!_OS Installer

Restart the computer again and choose your **USB drive** from the boot menu.

The Pop!_OS installer will load and you’ll get a graphical setup screen.

---

## Step 6 — Install Pop!_OS

You’ll be asked how you want to install the system.

I chose:

```
Clean Install
```

This wipes the drive and installs Pop!_OS fresh.

After that you’ll:

- Create your username
- Set a password
- Choose install location

The installer handles the rest.

---

## Step 7 — Reboot and Remove the USB

Once installation finishes the system will ask you to reboot.

Remove the USB drive when prompted so it boots into your new Pop!_OS system.

At this point you’re officially running Linux.

---

## Step 8 — Update the System

First thing I always do on a new Linux install is update everything.

Open a terminal and run:

```
sudo apt update
sudo apt upgrade
```

---

## Step 9 — Fix and Set Up My Other Drives

After the install I realized my other hard drives weren’t set up yet. Pop!_OS could see them, but they still had old Windows partitions.

First I checked all my drives with:

```
lsblk
```

Then I opened the **Disks** utility included with Pop!_OS.

Since the drives were previously used with Windows, I had to:

1. Delete the old partitions  
2. Create new partitions  
3. Format them using the **ext4 filesystem**

Once formatted, the drives mounted under:

```
/media/username/
```

Mine show up as:

```
/media/notyourdad/Node one
/media/notyourdad/Node two
```

I now use those drives for things like:

- virtual machines
- lab environments
- project files
- general storage

This keeps my **main system drive clean** while the other drives handle lab work.

---

## Final Thoughts

Switching from Windows to Pop!_OS honestly wasn’t nearly as scary as I expected. The first couple hours involved some learning and troubleshooting, but once you start understanding how Linux handles things like drives, permissions, and services, it actually starts to make a lot of sense.

If you’re curious about Linux, cybersecurity, or just want more control over your system, I definitely recommend giving Pop!_OS a try.

At this point I can honestly say **I love it**. The more I use it and learn how things work under the hood, the more comfortable it feels. I went into this thinking I might end up going back to Windows at some point, but after getting everything set up the way I want it, I really don’t see myself switching back.
