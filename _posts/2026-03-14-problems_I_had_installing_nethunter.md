---
title: Problems I Hit Installing Kali NetHunter on the OnePlus 7 Pro
date: 2026-03-14
categories: [android, kali, nethunter]
tags: [kali, nethunter, troubleshooting, oneplus7pro]
---

When installing Kali NetHunter on my OnePlus 7 Pro I ran into several problems that slowed the process down.

Most guides only show the perfect install path, but the issues are usually what take the longest to figure out.

Here are the main problems I ran into.

---

## OxygenOS 11 Compatibility

The first issue was starting on **OxygenOS 11**.

I originally tried installing NetHunter directly but ran into compatibility problems. Most working NetHunter kernels for the OnePlus 7 series are built for **Android 10 / OxygenOS 10**.

The solution was downgrading the phone using the MSM tool, which restores the device to **Android 9**, and then updating it to **OxygenOS 10**.

---

## MSM Tool Timing Window

The MSM tool works well but there is a small timing issue.

After putting the phone into **EDL mode**, you only have about **10–20 seconds before the phone reboots itself**.

If you miss that window the flash fails.

The easiest way to avoid this is to:

- open the MSM tool first
- install the drivers
- click start immediately after plugging the phone in

---

## Bootloader Unlock Wipes the Device

Unlocking the bootloader resets the phone completely.

```bash
adb reboot bootloader
fastboot oem unlock
```

This wipes the device, so anything important should be backed up first.

---

## TWRP Could Not Access Internal Storage

When booting into **TWRP**, the internal storage could not be browsed normally.

Trying to move through directories would return to the root storage list.

This happens when **TWRP cannot decrypt the Android data partition**.

Instead of troubleshooting the encryption issue, I used **ADB sideload** to flash the kernel.

---

## Flashing the Kernel with ADB Sideload

Boot TWRP:

```bash
fastboot boot twrp.img
```

Inside TWRP go to:

```
Advanced → ADB Sideload
```

Then run from the computer:

```bash
adb sideload kernel-nethunter-20230215_094959-oneplus7-oos-ten.zip
```

This worked immediately and avoided the storage problem.

---

## WiFi Adapter Compatibility

I tested a **MediaTek MT7612U adapter**.

The adapter showed up when checking USB devices:

```bash
lsusb
```

However, no wireless interface appeared.

This means the adapter was detected but the necessary driver support was not available in the kernel.

---

## Final Result

After completing the setup I had:

- rooted OnePlus 7 Pro
- OxygenOS 10
- NetHunter kernel installed
- Kali NetHunter apps running
- Kali chroot environment working
- USB OTG working

The biggest lesson from this setup was that **most of the time is spent troubleshooting small problems rather than the installation itself**.
