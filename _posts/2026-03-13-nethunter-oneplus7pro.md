---
title: Installing Kali NetHunter on a OnePlus 7 Pro (From OxygenOS 11)
date: 2026-03-13
categories: [android, kali, nethunter]
tags: [kali, nethunter, oneplus7pro, android, rooting]
---

This took me a couple days to figure out so I’m writing it down in case it helps someone else.

My goal was to run Kali NetHunter on a OnePlus 7 Pro so I could use Kali tools and external hardware like USB WiFi adapters.

Originally my phone was running OxygenOS 11, but NetHunter works much more reliably on OxygenOS 10, so the first step was downgrading the phone.

---

## Tools I installed on my Pop!_OS machine

Before doing anything with the phone I installed the Android tools.

```bash
sudo apt update
sudo apt install android-tools-adb android-tools-fastboot
```

These tools allow your computer to communicate with the phone.

---

## Step 1 — Downgrade the phone with the MSM tool

This step requires a Windows machine.

Download the MSM downgrade tool:

https://onepluscommunityserver.com/list/Unbrick_Tools/OnePlus_7_Pro/T-Mobile_GM31CB/

Install the Qualcomm USB drivers:

https://drive.google.com/file/d/1zKPFtcc2X_Nf70mcvn9TBu60bHl6Q3cP/view

Install the drivers first.

Open the MSM executable.

Put the phone into **EDL mode**, plug it into the computer, and press **Start** in the MSM tool.

Important note: you only have about **10–20 seconds before the phone automatically reboots**, so have everything ready before plugging the phone in.

When the process finishes the phone will be restored to **Android 9**.

---

## Step 2 — Update the phone to OxygenOS 10

Once the phone boots again update it to **OxygenOS 10**.

NetHunter kernels for the OnePlus 7 series are built around the Android 10 / OxygenOS 10 kernel which is why this version is important.

---

## Step 3 — Unlock the bootloader

Enable **Developer Options** and turn on:

- OEM unlocking
- USB debugging

Reboot to the bootloader:

```bash
adb reboot bootloader
```

Unlock the bootloader:

```bash
fastboot oem unlock
```

This will wipe the phone.

---

## Step 4 — Download the stock boot image

Download the stock boot image here:

https://androidfilehost.com/?fid=1395089523397968592

The file needed is:

```
boot.img
```

---

## Step 5 — Root the phone with Magisk

Download Magisk:

https://github.com/topjohnwu/magisk/releases

Install Magisk on the phone.

Inside Magisk choose **Patch Boot Image** and select the `boot.img`.

Magisk will create:

```
magisk_patched.img
```

Copy the patched image back to your computer.

Flash it with fastboot:

```bash
fastboot flash boot magisk_patched.img
```

Reboot the phone.

The phone should now be rooted.

---

## Step 6 — Install the NetHunter Store

Download the NetHunter Store:

https://store.nethunter.com/

From the store install:

- NetHunter App
- NetHunter Terminal

---

## Step 7 — Install the Kali chroot

Open the **NetHunter App**.

Inside the app install the **Kali chroot environment**.

After the install finishes open **NetHunter Terminal** and launch Kali.

Test that Kali works:

```bash
apt update
```

If this runs successfully the Kali environment is working correctly.

---

## Step 8 — Download the NetHunter kernel

Download the kernel here:

https://androidfilehost.com/?fid=4279422670115718693

The kernel used:

```
kernel-nethunter-20230215_094959-oneplus7-oos-ten.zip
```

---

## Step 9 — Flash the NetHunter kernel with TWRP

Reboot the phone to the bootloader:

```bash
adb reboot bootloader
```

Boot TWRP:

```bash
fastboot boot twrp.img
```

Inside TWRP go to:

**Advanced → ADB Sideload**

Swipe to start sideload.

Then from your computer run:

```bash
adb sideload kernel-nethunter-20230215_094959-oneplus7-oos-ten.zip
```

After the flash finishes reboot the phone.

---

## Step 10 — Verify the NetHunter kernel

Run:

```bash
adb shell uname -r
```

Expected output:

```
4.14.117-Draco-Re4son-1.1
```

This confirms the NetHunter kernel installed successfully.

---

## Final Result

After completing everything I had:

- rooted OnePlus 7 Pro
- OxygenOS 10
- NetHunter kernel installed
- Kali NetHunter apps running
- Kali chroot environment working
- USB OTG working

At this point the phone was fully running **Kali NetHunter**.
