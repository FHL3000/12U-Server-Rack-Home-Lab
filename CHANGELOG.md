# Changelog

All notable changes to the **12U Server Rack Home Lab** project will be documented in this file. This follows the [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) principles.

---
### Changed:
- Improved rack accessibility by positioning **PDU** at the bottom.

### Removed:
- N/A

## [Unreleased]
### Planned Features:
- Install and configure **Proxmox VE** for virtualization.
- Set up VLANs on the **Aruba 24-Port Managed Switch**.
- Deploy virtual machines: **Windows Server**, **Ubuntu Server**, and **pfSense**.
- Experiment with firewall rules and advanced monitoring tools.

---
## [1.1.0] - 2025-02-08
### Added:
- Deployed **Proxmox VE** using **iDRAC** for professional-grade OS installation.
- Configured **iDRAC** for remote management and streamlined deployment process.
- Documented the installation process for **Proxmox VE** in `/docs/proxmox-setup.md`.


## [1.0.0]  02-03-2025 to 02-07-2025
### Added:
- Initial setup of the **12U server rack**, including:
  - Mounted **Dell PowerEdge R230 Server**, **Raspberry Pi**, **ASUS Router**, and **Aruba Switch**.
  - Installed **16-port patch panel** for structured cabling.
  - Integrated **adjustable-depth Tec Mojo 12U rack**.
- Completed hardware upgrades:
  - Upgraded CPU to **Intel Xeon E3-1270 V6**.
  - Installed **32GB ECC RAM** and dual **1TB SSDs**.
  - Applied **Kryonaut thermal grease** for improved cooling.
- Structured cabling:
  - Crimped and tested custom Ethernet cables.
  - Connected devices to the patch panel and switch:
    - **Raspberry Pi:** Patch Panel Port 9 → Switch Port 10.
    - **Router:** Patch Panel Port 10 → Switch Port 12.
    - **iDRAC:** Patch Panel Port 11 → Switch Port 14.
    - **Server GB1 (Uplink):** Patch Panel Port 12 → Switch Port 16.
- Organized power and data cables with braided sleeves and Velcro ties.


---
