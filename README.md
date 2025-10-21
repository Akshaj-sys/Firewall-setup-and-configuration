# pfSense Firewall Setup and Configuration

**Objective**

The purpose of this project was to set up and configure pfSense firewall in a virtualized lab environment using Oracle VirtualBox. The goal was to simulate a controlled network environment where firewall rules could be applied, tested, and verified against both legitimate traffic (using ping tests) and simulated attacks (using Nmap scans from Kali Linux).

By the end of the project, the firewall was successfully configured to:

- Provide secure network segmentation.
- Allow legitimate traffic from the internal LAN to the Internet.
- Log and block malicious or suspicious traffic.
- Strengthen understanding of network defense strategies in a home lab setup.

**Skills Learned**

- Network security
- Access protocol
- logging and monitoring
- pfsense

**Tools Used**

- pfSense- open-source firewall and router software.
- Oracle VirtualBox- a virtualization platform.
- Ubuntu Linux VM- workstation for testing internet and LAN connectivity.
- Kali Linux VM- used to simulate attacks with Nmap.
- Nmap- port scanner and network reconnaissance tool.
- 7-Zip- used to extract the Netgate installer image.
- Command-line utilities- ping, traceroute for testing.

**Steps & Screenshots**

*Step 1: pfSense ISO Download & VM Creation*

- Downloaded pfSense Community Edition (amd64) installer ISO from the official Netgate website (cost: $0).
- Extracted the ISO using 7-Zip.
- Created a new Virtual Machine in VirtualBox:
  - Name: pfSense-firewall
  - Type: BSD
  - Version: FreeBSD (64-bit)
  - Memory: 2048 MB RAM
  - Storage: 10 GB virtual hard disk
- Added the pfSense ISO in the storage section.
- Configured networking:
  - Adapter 1 → NAT
  - Adapter 2 → Host-Only Adapter (with Promiscuous Mode = Allow VMs).
<img width="1171" height="703" alt="Screenshot 2025-08-17 201918" src="https://github.com/user-attachments/assets/8c855b82-dcb1-4d46-8091-c34395c25edc" />


*Step 2: pfSense Installation & Interface Setup*

- Booted the VM and installed pfSense with default installation settings.
- Powered off the VM and removed the ISO from storage to avoid reinstall.
- Restarted pfSense VM → Assigned interfaces manually:
  - em0 → WAN
  - em1 → LAN
- Configured interface IP addresses:
  - WAN → 10.0.2.1 (DHCP enabled).
  - LAN → 192.168.56.1.

This ensured pfSense would act as a gateway between the internet (WAN side) and internal VMs (LAN side).

*Step 3: Configuring Ubuntu & Kali Linux VMs*

- Opened Ubuntu VM → added Adapter 2: Host-Only Adapter (Promiscuous Mode: Allow VMs).
- Repeat the same steps for Kali Linux VM.
- Result: All three machines (pfSense, Ubuntu, Kali) were present on the same LAN via 192.168.56.0/24 subnet.

*Step 4: Accessing pfSense GUI*

- Opened browser in Ubuntu VM → accessed pfSense at: &lt;<http://192.168.56.1>&gt;
- Default credentials: admin / pfsense.
- Completed the setup wizard and set up a stronger password
<img width="1187" height="398" alt="Screenshot 2025-08-16 180702" src="https://github.com/user-attachments/assets/0d0b9f40-6a5b-49ef-ae4c-fd9cc8ea2e35" />


*Step 5: Firewall Rules Configuration*

- By default, the WAN interface had rules:
  - Block private networks
  - Block bogon networks
- By default, the LAN interface had rules:
  - Anti-Lockout Rule
  - By default, allow LAN to access any rule
  - Default allow LAN IPv6 to any
- Added two custom rules on LAN:
  - Log and Block Rule (logs and rejects connections).
  - Reject the Traffic Rule for specific cases.
  
<img width="1194" height="593" alt="Screenshot 2025-08-17 201846" src="https://github.com/user-attachments/assets/ff143ece-a046-4f9b-88d3-281731b97d28" />

*Step 6: Connectivity Verification*

Validated firewall and routing functionality by running pings:

*Step 7: Firewall Testing with Nmap*

- From Kali Linux, simulated attack with: nmap -sS -p 1-200 192.168.56.1
- pfSense detected the scan and blocked packets as per the configured rules.

<img width="1904" height="764" alt="Screenshot 2025-08-17 201638" src="https://github.com/user-attachments/assets/1cd57424-ece9-4da7-85de-a125e9f4df1b" />

<img width="1154" height="685" alt="Screenshot 2025-08-17 201015" src="https://github.com/user-attachments/assets/baf52289-c1de-4ba1-9327-c99c8db8fce0" />


**Conclusion**

This project successfully demonstrated the setup, configuration, and testing of pfSense firewall in a virtual lab.

<img width="946" height="695" alt="Screenshot 2025-09-16 202527" src="https://github.com/user-attachments/assets/7228f3cb-707b-440b-a692-0099413d3a8c" />


**Key takeaways:**

- PfSense installation and interface assignment were crucial for proper connectivity.
- Firewall rules were tested and validated against real traffic.
- The system effectively logged and blocked Nmap scans from Kali Linux, confirming that the firewall was functioning as intended.

This lab now serves as a foundation for future projects such as:

- Integrating with IDS/IPS tools (e.g., Snort, Suricata).
- Designing advanced incident response simulations.
