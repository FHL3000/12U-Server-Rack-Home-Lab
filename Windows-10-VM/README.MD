# Windows 10 Installation on Proxmox Hypervisor

This document outlines how I installed **Windows 10 Pro** on a virtual machine using the **Proxmox VE hypervisor**. It includes complete configuration steps, driver setup using VirtIO, and future plans for optimization and feature enhancement. This VM is intended for IT labs, certification prep, and general system administration practice.

---

<div align="center">

## Requirements

<p align="center">
  <img src="https://raw.githubusercontent.com/FHL3000/12U-Server-Rack-Home-Lab/main/Windows-10-VM/Install-Images/Screenshots/1-Windows-ISO-Download.png" width="250"/>
  <img src="https://raw.githubusercontent.com/FHL3000/12U-Server-Rack-Home-Lab/main/Windows-10-VM/Install-Images/Screenshots/2-VirtIO-Download.png" width="250"/>
  <img src="https://raw.githubusercontent.com/FHL3000/12U-Server-Rack-Home-Lab/main/Windows-10-VM/Install-Images/Screenshots/3-Upload-ISO-Proxmox.png" width="250"/>
</p> 

| Item         | Description |
|--------------|-------------|
| Proxmox VE   | Hypervisor installed and accessible |
| Windows 10 ISO | Downloaded from [Microsoft](https://www.microsoft.com/software-download/windows10) |
| VirtIO ISO   | Downloaded from [Fedora VirtIO Drivers](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/latest-virtio/) |
| VM Storage   | Minimum 32GB disk, 8GB RAM recommended |
| Internet     | For Windows updates and guest tools setup |

</div>

---

## VM Configuration in Proxmox


### System

  <img src="https://github.com/FHL3000/12U-Server-Rack-Home-Lab/blob/a51dcc8d17fb8ca52944057a7b3edf03d53de667/Windows-10-VM/Install-Images/Screenshots/5-System-Selections.png?raw=true" alt="System Selection Screenshot" width="400"/>
</div>

<div style="display: flex; align-items: flex-start; gap: 20px;">
  <table>
    <thead>
      <tr><th>Option</th><th>Value</th></tr>
    </thead>
    <tbody>
      <tr><td>BIOS</td><td>OVMF (UEFI)</td></tr>
      <tr><td>Machine</td><td>q35</td></tr>
      <tr><td>Add EFI Disk</td><td>Yes</td></tr>
      <tr><td>Add TPM</td><td>Yes (TPM 2.0)</td></tr>
      <tr><td>Storage</td><td>local or local-lvm</td></tr>
    </tbody>
  </table>

<table>
  <tr>
    <td>

      <table>
        <thead>
          <tr><th>Option</th><th>Value</th></tr>
        </thead>
        <tbody>
          <tr><td>BIOS</td><td>OVMF (UEFI)</td></tr>
          <tr><td>Machine</td><td>q35</td></tr>
          <tr><td>Add EFI Disk</td><td>Yes</td></tr>
          <tr><td>Add TPM</td><td>Yes (TPM 2.0)</td></tr>
          <tr><td>Storage</td><td>local or local-lvm</td></tr>
        </tbody>
      </table>

    </td>
    <td style="vertical-align: top; padding-left: 20px;">
      <img src="https://raw.githubusercontent.com/FHL3000/12U-Server-Rack-Home-Lab/a51dcc8d17fb8ca52944057a7b3edf03d53de667/Windows-10-VM/Install-Images/Screenshots/5-System-Selections.png" alt="System Selection Screenshot" width="350">
    </td>
  </tr>
</table>

### Disks
| Option | Value |
|--------|-------|
| Bus/Device | SCSI (VirtIO) |
| Disk Size | 32 GiB (minimum) |
| IO Thread | Enabled |

### CPU
| Option | Value |
|--------|-------|
| Sockets | 1 |
| Cores | 2 |
| Type | host (recommended for performance) |

### Memory
| Option | Value |
|--------|-------|
| RAM | 8192 MiB (8GB) |

### Network
| Option | Value |
|--------|-------|
| Bridge | vmbr0 |
| Model | VirtIO (paravirtualized) |

---

## Installation Steps

### 1. Boot the VM from ISO
I started the VM using the mounted Windows 10 ISO.

### 2. Skip Product Key
I clicked **"I don’t have a product key"** during setup.

### 3. Choose Edition
I selected **Windows 10 Pro x64** for full feature support.

### 4. Custom Install
I used **Custom: Install Windows only** to perform a clean installation.

### 5. Load VirtIO Storage Driver
At the disk selection screen, I clicked **Load Driver**, then navigated to:
```
D:\vioscsi\w10\amd64\viostor.inf
```
After selecting the correct driver, the virtual hard drive appeared.

### 6. Complete Installation
I selected the disk and completed the installation as normal.

---

## Post-Install Network Setup
During setup, Windows did not initially detect the VirtIO NIC. I proceeded with offline setup by clicking **"I don’t have internet"**.

After reaching the desktop:
1. I opened File Explorer and navigated to:
```
D:\NetKVM\w10\amd64
```
2. I right-clicked on `netkvm.inf` and selected **Install**
3. The Ethernet adapter came online successfully

---

## Optional Enhancements (Planned for Later)
- [ ] Install `virtio-win-guest-tools.exe` to enable balloon drivers, video, and QEMU guest agent
- [ ] Enable QEMU Agent under Proxmox VM > Options
- [ ] Run Windows Updates to patch the system
- [ ] Adjust system scaling and resolution for optimal VM display
- [ ] Take a Proxmox VM snapshot of this clean install state
- [ ] Set up and test RDP connectivity and shared clipboard via QEMU tools
- [ ] Begin documenting hands-on labs such as software troubleshooting and Group Policy configuration

---

## Screenshots (To Be Added)
I will insert step-by-step visuals for the following sections:
- ISO Selection
- BIOS/TPM Configuration
- Storage Driver Load Step
- Network Driver Install Step
- Final Connection Confirmation

---

## License
This project is part of my personal home lab and learning documentation, shared publicly to demonstrate hands-on experience in system setup and virtualization.

---

## Status
> 🟩 Windows 10 VM operational and connected
> 🟨 Additional driver installations and optimizations pending


