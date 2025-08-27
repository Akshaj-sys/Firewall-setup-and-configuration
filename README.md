**pfSense Firewall Setup and Configuration**

**Objective**

The purpose of this project was to **set up and configure pfSense firewall** in a virtualized lab environment using Oracle VirtualBox. The goal was to simulate a controlled network environment where firewall rules could be applied, tested, and verified against both legitimate traffic (using ping tests) and simulated attacks (using Nmap scans from Kali Linux).

By the end of the project, the firewall was successfully configured to:

- Provide secure network segmentation.
- Allow legitimate traffic from the internal LAN to the internet.
- Log and block malicious or suspicious traffic.
- Strengthen understanding of network defense strategies in a homelab setup.

**Skills Learned**

- Installation and deployment of **pfSense firewall** on VirtualBox.
- Assigning and configuring **network interfaces** for WAN and LAN.
- Configuring IP addressing schemes and enabling **DHCP** for WAN.
- Accessing and managing the **pfSense Web GUI**.
- Creating, applying, and testing **firewall rules** (log, block, reject).
- Using **ping** to validate network connectivity.
- Performing **Nmap scans** from Kali Linux to simulate attacks.
- Analyzing **pfSense system logs** to detect and confirm blocked traffic.
- Strengthened problem-solving and troubleshooting skills in virtualized environments.

**Tools Used**

- **pfSense** (open-source firewall and router software).
- **Oracle VirtualBox** (virtualization platform).
- **Ubuntu Linux VM** (workstation to test internet and LAN connectivity).
- **Kali Linux VM** (used to simulate attacks with Nmap).
- **Nmap** (port scanner and network reconnaissance tool).
- **7-Zip** (used to extract Netgate installer image).
- **Command-line utilities** (ping, traceroute for testing).

**Steps & Screenshots**

**Step 1: pfSense ISO Download & VM Creation**

- Downloaded **pfSense Community Edition (amd64)** installer ISO from the official Netgate website (cost: $0).
- Extracted the ISO using **7-Zip**.
- Created a new Virtual Machine in **VirtualBox**:
  - Name: pfsense-firewall
  - Type: BSD
  - Version: FreeBSD (64-bit)
  - Memory: **2048 MB RAM**
  - Storage: **10 GB virtual hard disk**
- Added the pfSense ISO in the storage section.
- Configured networking:
  - **Adapter 1** → NAT
  - **Adapter 2** → Host-Only Adapter (with Promiscuous Mode = Allow VMs).

<img width="1171" height="703" alt="Screenshot 2025-08-17 201918" src="https://github.com/user-attachments/assets/5b088a76-79e5-46ea-8da9-a2a926aaa519" />


**Step 2: pfSense Installation & Interface Setup**

- Booted the VM and installed pfSense with default installation settings.
- Powered off the VM and removed the ISO from storage to avoid reinstall.
- Restarted pfSense VM → Assigned interfaces manually:
  - **em0 → WAN**
  - **em1 → LAN**
- Configured interface IP addresses:
  - WAN → 10.0.2.1 (DHCP enabled).
  - LAN → 192.168.56.1.

This ensured pfSense would act as a gateway between the internet (WAN side) and internal VMs (LAN side).

**Step 3: Configuring Ubuntu & Kali Linux VMs**

- Opened Ubuntu VM → added **Adapter 2: Host-Only Adapter** (Promiscuous Mode: Allow VMs).
- Repeated the same for Kali Linux VM.
- Result: All three machines (pfSense, Ubuntu, Kali) were on the same LAN via **192.168.56.0/24 subnet**.


**Step 4: Accessing pfSense GUI**

- Opened browser in Ubuntu VM → accessed pfSense at:
- <http://192.168.56.1>
- Default credentials: admin / pfsense.
- Completed **setup wizard** and changed to a stronger password.

<img width="1187" height="398" alt="Screenshot 2025-08-16 180702" src="https://github.com/user-attachments/assets/e7cd2322-8c78-4821-bcf7-4c34d183327b" />


**Step 5: Firewall Rules Configuration**

- By default, WAN interface had rules:
  - **Block private networks**
  - **Block bogon networks**
- By default, LAN interface had rules:
  - **Anti-Lockout Rule**
  - **Default allow LAN to any**
  - **Default allow LAN IPv6 to any**
- Added **two custom rules** on LAN:
  - **Log and Block Rule** (logs and rejects connections).
  - **Reject Traffic Rule** for specific cases.

<img width="1194" height="593" alt="Screenshot 2025-08-17 201846" src="https://github.com/user-attachments/assets/64cadfab-934c-47cb-9d85-0d15d115b0eb" />


**Step 6: Connectivity Verification**

Validated firewall and routing functionality by running pings:

- ping 8.8.8.8 (Google DNS) 
- ping google.com (DNS resolution) 
- ping 192.168.56.1 (LAN gateway) 


**Step 7: Firewall Testing with Nmap**

- From Kali Linux, simulated attack with:
- nmap -sS -p 1-200 192.168.56.1
- pfSense detected the scan and blocked packets as per configured rules.

<img width="1904" height="764" alt="Screenshot 2025-08-17 201638" src="https://github.com/user-attachments/assets/aa085a73-dd3f-4dc9-a4e5-3c56a7c56d62" />


<img width="1154" height="685" alt="Screenshot 2025-08-17 201015" src="https://github.com/user-attachments/assets/846d35f2-f81a-4295-aa54-13ceb8697918" />


**Conclusion**

This project successfully demonstrated the **setup, configuration, and testing of pfSense firewall** in a virtual lab.

Key takeaways:

- pfSense installation and interface assignment were crucial for proper connectivity.
- Firewall rules were tested and validated against real traffic.
- The system effectively **logged and blocked Nmap scans** from Kali Linux, confirming that the firewall was functioning as intended.

This lab now serves as a foundation for future projects such as:

- Integrating with **IDS/IPS tools** (e.g., Snort, Suricata).
- Designing advanced **incident response simulations**.
