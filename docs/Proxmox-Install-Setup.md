# Proxmox Installation & Initial Setup

## Overview
This document outlines my experience installing and setting up **Proxmox VE** on my **Dell PowerEdge R230** server. It covers everything from installation, networking, VM setup, and optimizations, based on what I configured in my home lab.

---

## 1. Installing Proxmox

### 1. Downloading Proxmox VE
I started by downloading the latest **Proxmox VE ISO** from the [Proxmox Download Page](https://www.proxmox.com/en/downloads). To create a bootable USB, I used:
- **Windows:** [Rufus](https://rufus.ie/)
- **Linux/macOS:**
  ```bash
  sudo dd if=proxmox-ve.iso of=/dev/sdX bs=4M status=progress
  ```

### 2. Installing Proxmox on My Server
Once my bootable USB was ready, I followed these steps:
1. Booted my server from the USB.
2. Selected **Install Proxmox VE**.
3. Chose the installation disk (**1TB SSD** in my case).
4. Set a **root password and email**.
5. Configured **network settings** (I opted for a static IP).
6. Finished installation and rebooted.

### 3. Accessing the Proxmox Web Interface
After installation, I accessed the Proxmox Web GUI using:
```bash
https://[proxmox-ip]:8006
```
I logged in with:
- **Username:** `root`
- **Password:** (the one I set during installation)

---

## 2. Post-Installation Configuration

### 1. Removing the Enterprise Repository (Since I Don't Have a Subscription)
```bash
sed -i 's/^deb/#deb/g' /etc/apt/sources.list.d/pve-enterprise.list
```

### 2. Adding the No-Subscription Repository & Updating the System
```bash
echo 'deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription' > /etc/apt/sources.list.d/pve-no-subscription.list
apt update && apt full-upgrade -y
```

### 3. Enabling the Proxmox Web GUI Without Subscription Warnings
```bash
sed -i '/proxmox.com/d' /etc/apt/sources.list.d/*
```

### 4. Enabling QEMU Guest Agent
To improve VM performance and communication with Proxmox, I installed:
```bash
apt install -y qemu-guest-agent
systemctl enable qemu-guest-agent --now
```

---

## 3. Configuring Networking

### 1. Setting Up a Network Bridge (`vmbr0`)
I needed my VMs to have external network access, so I configured a network bridge:
```bash
nano /etc/network/interfaces
```
- My static IP configuration:
```ini
auto vmbr0
iface vmbr0 inet static
  address 192.168.1.100/24
  gateway 192.168.1.1
  bridge-ports eno1
  bridge-stp off
  bridge-fd 0
```
- Applied changes:
```bash
systemctl restart networking
```

### 2. Assigning Network to VMs
When creating a VM, I made sure to select **`vmbr0`** as the network adapter.

---

## 4. Configuring Storage

### 1. Checking Storage Layout
```bash
lsblk
```

### 2. Expanding Local-LVM for VM Storage
```bash
lvextend -l +100%FREE /dev/pve/data
resize2fs /dev/pve/data
```

---

## 5. Creating a Windows 11 VM

### 1. Uploading the Windows 11 ISO & VirtIO Drivers
I uploaded `Win11_24H2_English_x64.iso` and `virtio-win.iso` to Proxmox via **Storage → Upload**.

### 2. Creating the VM
I configured the VM as follows:
- **OS:** `Microsoft Windows 11/2022`
- **BIOS:** `OVMF (UEFI)`
- **TPM 2.0:** Enabled for Windows 11 compliance
- **Disk:** `VirtIO SCSI`
- **Network:** `VirtIO (paravirtualized)`

### 3. Installing Windows 11 & VirtIO Drivers
During installation, I had to load **VirtIO storage drivers** manually:
```bash
D:\viostor\w11\amd64
```
After Windows was installed, I installed the network drivers:
```bash
D:\NetKVM\w11\amd64
```
Lastly, I installed the VirtIO guest tools for better performance.

---

## 6. Security & Optimization

### 1. Enabling Automatic Updates
```bash
echo "APT::Periodic::Update-Package-Lists \"1\";" | tee /etc/apt/apt.conf.d/10periodic
```

### 2. Configuring a Basic Firewall (`ufw`)
```bash
apt install ufw -y
ufw default deny incoming
ufw default allow outgoing
ufw allow 8006/tcp  # Allow Proxmox Web GUI access
ufw enable
```

### 3. Setting Up Backups
I scheduled daily VM backups via **Datacenter → Backup**, targeting external storage.

---

## 7. Final Steps & Testing

After setup, I ran a few tests:
- Verified connectivity:
```bash
ping 8.8.8.8
```
- Took a snapshot of my Windows VM before making further changes.
- Monitored Proxmox logs:
```bash
tail -f /var/log/syslog
```

With everything set up, my Proxmox home lab is fully operational!
