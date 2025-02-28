⬛️ Initial Wi-Fi & Network Speed Test Results

## Overview
This document details the **Wi-Fi performance**, **network throughput**, and **ISP speed test** results from different locations within the network. The tests include:

▪️ **Wi-Fi iPerf3 throughput tests**  
▪️ **Speed tests between Raspberry Pi, Home Lab, and ISP Router**  
▪️ **ISP Internet speed tests with bandwidth limitations**  
▪️ **Analysis of potential interference affecting Wi-Fi performance**  
▪️ **Planned Wi-Fi optimizations for improved performance**  

## Network Architecture
▪️ **This setup originally consisted of two separate subnets**:  
▫️ **Home Lab Network** – Dedicated for lab services and network testing.  
▫️ **General Home Network** – Used for personal devices, IoT, and general internet access.  
▪️ **The goal is to integrate VLAN segmentation to enhance security and network efficiency**.  

---

## Home Lab Setup  
▪️ **All critical home lab components are wired** in a **12U rack** for stability and performance.  
▪️ **Wi-Fi is primarily used for mobile devices, laptops, and non-critical IoT devices**.  
▪️ **Future optimizations will improve Wi-Fi segmentation, efficiency, and coverage**.  

---

## Wi-Fi iPerf3 Speed Tests
Wi-Fi performance was tested using **iPerf3** from different locations.  

**Wi-Fi Performance (Upstairs)** 
▪️ **Total Transfer**: **166 MB** (Sender) / **164 MB** (Receiver)  
▪️ **Bitrate**: **139 Mbps (Sender) / 137 Mbps (Receiver)**  

📌 **Observations:**  
▪️ **Fluctuating speeds** (109 - 179 Mbps) suggest **signal degradation or interference**.  
▪️ **Possible interference from a subnetwork sharing Wi-Fi channels**.  
▪️ **Future improvements will help mitigate interference**.  

 **Wi-Fi Performance (Downstairs)**  
▪️ **Total Transfer**: **290 MB** (Sender) / **287 MB** (Receiver)  
▪️ **Bitrate**: **243 Mbps (Sender) / 240 Mbps (Receiver)**  

📌 **Observations:**  
▪️ **Higher stability and speeds compared to upstairs**.  
▪️ **Planned improvements will further optimize overall Wi-Fi coverage**.  

---

⬛️ Raspberry Pi Speed Tests  

 **Speed Test: Raspberry Pi to Home Lab**  
![Pi to Home Lab](../SpeedTest%20PI%20to%20Homelab.png)  

▪️ **Download Speed:** `33.83 Mbps`  
▪️ **Upload Speed:** `1.76 Mbps`  

 **Speed Test: Raspberry Pi to ISP Router**  
![Pi to ISP Router](../SpeedTest%20Pi%20to%20ISP%20router.png)  

▪️ **Download Speed:** `33.87 Mbps`  
▪️ **Upload Speed:** `1.67 Mbps`  

📌 **Observations:**  
▪️ **Download speeds are stable**, but **upload speeds are ISP-capped**.  

---

⬛️ ISP Speed Test Results  

| Test Location | Download Speed | Upload Speed |
|--------------|---------------|-------------|
| **Test 1** | **33.83 Mbps** | **1.76 Mbps** |
| **Test 2** | **33.87 Mbps** | **1.67 Mbps** |

 **ISP Bandwidth Cap Limitations:**  
▪️ **Download speeds (~33 Mbps) match ISP's plan**.  
▪️ **Upload speeds (~1.7 Mbps) are limited due to ISP restrictions**.  
▪️ **Low upstream bandwidth affects cloud backups and remote access**.  

---

⬛️ Planned Wi-Fi Optimizations
To **improve Wi-Fi performance** and **reduce interference**, the following enhancements will be implemented:  

 **1. VLAN Segmentation with Multiple SSIDs**  
▪️ **Isolate traffic** for better security and performance.  
▪️ **Dedicated SSIDs for IoT, home lab, guests, and personal devices**.  

 **2. QoS Optimization**  
▪️ **Prioritize latency-sensitive traffic** (video calls, gaming, work devices).  
▪️ **Set bandwidth limits** for low-priority devices.  

 **3. Centralized Access Point & Mesh Extenders**  
▪️ **Deploy a central AP** for better coverage.  
▪️ **Use mesh extenders** to eliminate Wi-Fi dead zones.  

 **4. Optimized Router Placement**  
▪️ **Reposition the router** to maximize coverage.  
▪️ **Avoid signal-blocking obstacles** like walls, furniture, and appliances.  

 **5. Eliminating Obstructions & Interference**  
▪️ **Check for subnetworks sharing Wi-Fi channels**.  
▪️ **Switch to less congested channels**.  
▪️ **Reduce interference from nearby devices (microwaves, Bluetooth, etc.)**.  

---

⬛️ Conclusions
✅ **Wi-Fi performance is stable but varies by location.**  
❌ **Upstairs speeds are lower due to possible interference and distance from the router.**  
❌ **ISP upload speeds are capped, limiting outbound traffic efficiency.**  
✅ **Critical home lab components are already wired in a 12U rack.**  
✅ **Planned Wi-Fi optimizations will significantly improve performance.**  

✅ **Next Steps**  
▪️ **Implement VLAN segmentation & multiple SSIDs**.  
▪️ **Optimize QoS settings to prioritize critical traffic**.  
▪️ **Deploy a centralized access point and mesh extenders**.  
▪️ **Reposition the router and remove physical obstructions**.  
▪️ **Check for channel conflicts and adjust Wi-Fi settings accordingly**.  
▪️ **Monitor improvements and conduct follow-up speed tests**.  

---

⬛️ Reference Files  
▪️ [`iperf3 Wifi Results Upstairs.png`](../iperf3%20Wifi%20Results%20Upstairs.png)  
▪️ [`iperf3 Wifi Results Downstairs.png`](../iperf3%20Wifi%20Results%20Downstairs.png)  
▪️ [`SpeedTest PI to Homelab.png`](../SpeedTest%20PI%20to%20Homelab.png)  
▪️ [`SpeedTest Pi to ISP router.png`](../SpeedTest%20Pi%20to%20ISP%20router.png)  
