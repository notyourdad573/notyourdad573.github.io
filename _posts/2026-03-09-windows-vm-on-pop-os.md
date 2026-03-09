---
title: "Setting Up a Windows Virtual Machine on Pop!_OS"
date: 2026-03-08
categories: [Linux, Homelab]
tags: [linux, pop-os, virtualization, kvm, homelab]
---

# Setting Up a Windows Virtual Machine on Pop!_OS

After switching my desktop over to Pop!_OS, one of the first things I wanted to do was get a Windows virtual machine running. Even though I’m moving more and more into Linux, there are still a few things that are easier to do in Windows, and having a VM makes that simple.

For lab work and cybersecurity stuff it also helps a lot. Being able to spin up another machine inside your system without touching the host is really useful.

Here’s how I set mine up.

## Why I Wanted a Windows VM

Even though I’m running Linux full time now, there are still a few situations where Windows is useful.

Things like:

- testing software
- running Windows only tools
- building lab environments
- breaking things safely without touching the host system

Running Windows inside a VM keeps my main system clean and lets me experiment without worrying about messing anything up.

## Step 1 Install Virtualization Tools

Pop!_OS supports KVM virtualization which is really fast since it uses hardware virtualization from your CPU.

First I installed the virtualization tools.

Open a terminal and run:

```
sudo apt update
sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients virt-manager bridge-utils
```

These packages install the main components needed for virtualization.

- KVM which acts as the hypervisor
- libvirt which manages virtual machines
- virt-manager which gives you a graphical interface to create and manage VMs

## Step 2 Enable the Virtualization Service

After installing everything I made sure the virtualization service was running.

```
sudo systemctl enable --now libvirtd
```

Then I checked the status.

```
systemctl status libvirtd
```

If everything is working you should see that the service is active and running.

## Step 3 Add Your User to the libvirt Group

To manage virtual machines without needing root permissions every time, I added my user to the libvirt group.

```
sudo usermod -aG libvirt $USER
```

After doing this you need to log out and log back in so the permission change applies.

## Step 4 Open Virtual Machine Manager

Now we can open the tool that actually manages the virtual machines.

```
virt-manager
```

This opens the Virtual Machine Manager interface.

Make sure it connects to:

```
QEMU/KVM System
```

If it shows no active connection you can add one from the menu.

Go to:

```
File → Add Connection
```

Then choose:

```
Hypervisor: QEMU/KVM
Connection: System
```

Once that is connected you are ready to create VMs.

## Step 5 Create the Windows VM

Inside Virtual Machine Manager:

1. Click Create a New Virtual Machine
2. Choose Local install media
3. Select your Windows ISO file
4. Assign memory and CPU cores
5. Choose where the virtual disk will be stored

I store my virtual machines on one of my secondary drives so my main system drive stays clean.

## Step 6 Install Windows

Once the VM starts it behaves just like a normal computer booting from a Windows installer.

Just follow the normal Windows installation process.

The VM will create its virtual disk and install Windows inside it.

## Why I Like This Setup

Running Windows inside a VM has a few big advantages.

- I can snapshot machines
- I can break things without ruining my system
- I can run multiple operating systems at the same time
- everything stays isolated from my host machine

It is also surprisingly fast because KVM uses hardware virtualization.

## Final Thoughts

After switching to Pop!_OS and getting virtualization working my desktop basically turned into a full lab environment.

I can run Linux, Windows, and whatever else I want on the same machine without touching my main system.

Between Pop!_OS and KVM this setup feels way more flexible than what I had before.

The more I use Linux the more I realize how much control it gives you over your system. Being able to build your own environment like this is pretty awesome.
