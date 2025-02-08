# 12U Server Rack Home Lab

## **Project Overview**
Welcome to the documentation for my **12U Server Rack Home Lab**! This project is a professional-grade setup designed to enhance my skills in IT infrastructure, virtualization, networking, and security. The goal is to build a scalable, hands-on learning environment to simulate enterprise environments.

---

## **Key Components**

### **Hardware**
- **Dell PowerEdge R230 Server:**
  - Upgraded with Intel Xeon E3-1270 V6, 32GB ECC RAM, and dual 1TB SSDs.
- **Aruba 24-Port Managed Switch:** For VLANs and network segmentation.
- **16-Port Patch Panel:** Structured cabling for modular connections.
- **ASUS Router:** For home network connectivity.
- **Raspberry Pi:** For lightweight tasks and DNS management.
- **Tec Mojo 12U Adjustable Depth Rack:** Holds all components securely.

### **Networking**
- **Custom Crimped Ethernet Cables:**
  - Precise, color-coded cables for clean connections.
  - Includes patch panel integration for modularity.
- **Cable Management:**
  - Routed power and data cables separately for reduced interference and a polished look.

---

## **Recent Updates**

### **1️⃣ Server Upgrade**
- **CPU:** Upgraded to Intel Xeon E3-1270 V6 for better performance.
- **RAM:** Replaced stock 8GB with 32GB ECC UDIMM.
- **Storage:**
  - 1TB Crucial MX500 SATA SSD for OS and critical data.
  - 1TB Vulcan Z QLC SATA SSD for virtualization storage.
- **Cooling:** Applied Kryonaut thermal grease for optimal cooling.
- **Drive Bays:** Installed SSD holders for secure storage integration.

### **2️⃣ Structured Cabling**
- **Patch Panel Integration:**
  - Raspberry Pi: Patch Panel Port 9 → Switch Port 10.
  - Router: Patch Panel Port 10 → Switch Port 12.
  - iDRAC: Patch Panel Port 11 → Switch Port 14.
  - Server GB1 (Uplink): Patch Panel Port 12 → Switch Port 16.
- **Custom Ethernet Cables:**
  - Crimped, tested, and labeled for clean and reliable connections.
- **Cable Management:**
  - Power and data cables routed separately, using braided sleeves and Velcro ties.

---

## **Project Features**
- **Virtualization:** Deploying and managing VMs with Proxmox VE, including Windows Server, Ubuntu Server, and pfSense.
- **Networking:** VLAN configurations for segmented traffic control and enhanced security.
- **Expandable Design:** Space for additional components and future upgrades.

---

## **Setup Gallery**
- Photos of the rack setup, devices, and structured cabling.
- Network diagrams showcasing connectivity and VLAN configurations.

---

## **Next Steps**
1. **iDRAC OS Deployment:** Install and configure Proxmox VE for virtualization.
2. **Device Configurations:**
   - Configure VLANs on the Aruba managed switch.
   - Set up and manage virtual machines for various use cases.
3. **Future Experiments:** Test firewall rules, intrusion detection, and advanced monitoring setups.

---

## **Feedback & Contributions**
I’m always open to feedback and suggestions for improving my home lab setup! Feel free to connect with me or share your thoughts.

---

## **Tags**
`#HomeLab` `#Networking` `#Virtualization` `#ServerSetup` `#12UHomeLab
