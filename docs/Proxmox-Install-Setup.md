# Proxmox Installation & Optimized Setup

## Overview
This document outlines my **Proxmox VE** installation and setup on a **Dell PowerEdge R230** server. It includes networking, backup strategy, performance optimizations, and VM configurations for my home lab.

---

## 1. Installing Proxmox

### - Downloading Proxmox VE
I downloaded the latest **Proxmox VE ISO** from the [Proxmox Download Page](https://www.proxmox.com/en/downloads) and created a bootable USB:
- **Windows:** [Rufus](https://rufus.ie/)
- **Linux/macOS:**
  ```bash
  sudo dd if=proxmox-ve.iso of=/dev/sdX bs=4M status=progress
  ```

### - Installing Proxmox on My Server
✔ Booted the server from the USB.  
✔ Selected **Install Proxmox VE**.  
✔ Chose the installation disk (**1TB SSD**).  
✔ Set a **root password and email**.  
✔ Configured **network settings** (static IP).  
✔ Finished installation and rebooted.  

### - Accessing the Proxmox Web Interface
Accessed Proxmox via:
```bash
https://[proxmox-ip]:8006
```
Login credentials:
- **Username:** `root`
- **Password:** (set during installation)

---

## 2. Post-Installation Configuration

### - Removing Enterprise Repository (No Subscription)
```bash
sed -i 's/^deb/#deb/g' /etc/apt/sources.list.d/pve-enterprise.list
```

### - Adding No-Subscription Repository & Updating System
```bash
echo 'deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription' > /etc/apt/sources.list.d/pve-no-subscription.list
apt update && apt full-upgrade -y
```

### - Enabling QEMU Guest Agent for VMs
```bash
apt install -y qemu-guest-agent
systemctl enable qemu-guest-agent --now
```

---

## 3. Configuring Networking

### - Setting Up a Network Bridge (`vmbr0`)
Configured the network bridge to allow VM network access:
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

### - Assigning Network to VMs
When creating a VM, I selected **`vmbr0`** as the network adapter.

---

## 4. Configuring Backup Strategy

### - Automated Snapshot and Full Backup Schedule
Configured a backup job with **ZSTD compression**:
✔ **Snapshots:**
  - **Daily:** Keep last **7 days**
  - **Weekly:** Keep last **4 weeks**
  - **Monthly:** Keep last **3 months**
✔ **Full Backups:**
  - **Weekly:** Keep **2 weeks**
  - **Monthly:** Keep **1 month**

### - Enabling Automatic Backup Cleanup
Proxmox automatically removes old backups:
- **Retention settings applied** to delete outdated snapshots/full backups.
- Storage usage monitored using:
  ```bash
  du -sh /var/lib/vz/dump/
  ```

---

## 5. Performance Optimizations

### - CPU Configuration
✔ **CPU Type:** Already set to **Host** to allow full hardware utilization.

### - Enabling TRIM for SSD Performance
To maintain SSD efficiency, I enabled TRIM:
```bash
fstrim -av
systemctl enable fstrim.timer
```

### - Optimizing Disk Performance
For better Windows VM disk performance, I changed disk caching:
- **Proxmox Web UI → VM → Hardware → Hard Disk → Cache Mode:** `Write Back`

### - Memory Optimization
- Increased Windows 11 VM RAM to **8192MB (8GB)** for improved performance.

---

## 6. Windows 11 VM Setup

### - Uploading Windows 11 ISO & VirtIO Drivers
Uploaded `Win11_24H2_English_x64.iso` and `virtio-win.iso` to Proxmox via **Storage → Upload**.

### - Creating the VM
- **OS:** `Microsoft Windows 11/2022`
- **BIOS:** `OVMF (UEFI)`
- **TPM 2.0:** Enabled
- **Disk:** `VirtIO SCSI`
- **Network:** `VirtIO (paravirtualized)`

### - Installing Windows 11 & VirtIO Drivers
During installation, I manually loaded the **VirtIO storage drivers**:
```bash
D:\viostor\w11\amd64
```
After Windows was installed, I installed the network drivers:
```bash
D:\NetKVM\w11\amd64
```
Lastly, I installed the VirtIO guest tools for better performance.

---

## 7. Future Plans & Next Steps

✔ **Set Up Storage Alerts** (to monitor backup space usage).  
✔ **Expand VM Lab**:
   - Add Linux-based VMs for testing server/networking setups.
   - Deploy a Windows Server VM for Active Directory testing.
✔ **Enhance Security**:
   - Implement SSH hardening & Fail2Ban.
   - Set up remote access VPN (Tailscale/WireGuard).
✔ **Monitor Performance**:
   - Deploy Grafana & Prometheus for resource tracking.

---

### **Summary**
This document reflects my complete **Proxmox VE setup, backup strategy, and performance optimizations**. My Proxmox home lab is now fully operational, with optimized configurations and efficient backup handling.

