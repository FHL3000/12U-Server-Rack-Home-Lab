# Proxmox VE Initial Setup

## **1️⃣ Installation Steps**
- Downloaded **Proxmox VE ISO** from [Proxmox Official Site](https://www.proxmox.com/en/downloads).
- Used **iDRAC Virtual Media** to mount the ISO and begin installation.

## **2️⃣ Hostname & Network Configuration**
- **Hostname:** `proxmox.home.lab`
- **Management IP:** `192.168.1.50/24`
- **Gateway:** `192.168.1.1`
- **DNS Servers:** `8.8.8.8, 1.1.1.1`

## **3️⃣ Storage Configuration**
- **Boot Drive:** `1TB Crucial MX500 SSD`
- **VM Storage:** `1TB Vulcan Z SSD`
- **File System:** `ext4` or `ZFS` (to be decided)

## **4️⃣ Next Steps**
- Verify network connectivity.
- Update repositories and install essential packages.
- Set up user access and SSH keys.

---
**📌 Notes:**  
This configuration ensures Proxmox VE is installed with a **static IP, hostname, and storage layout**, making it ready for further customization.  
