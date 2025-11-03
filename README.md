# SIEM-LAB

## SIEM + Active Directory Lab

## Overview
A hands-on lab to build:
- Active Directory setup for centralized authentication
- Splunk SIEM deployment for log collection and threat analysis
- Wireshark for traffic inspection
- Python automation for scripting and efficiency

# Lab Architecture
## Component    - Description
Windows Server - Domain Controller with Active Directory, DNS, and DHCP
Windows 11     - Domain-joined workstation
Splunk         - SIEM platform for log ingestion and analysis
Wireshark      - Network packet capture and analysis tool
Python         - Automation scripting environment

# Network Configuration
## VM            - IP Address  - Role               - Network
Windows Server   - 10.1.10.x  - Domain Controller  -  Host-only

Windows 11       - 10.1.10.x  - Domain Workstation - Host-only

Subnet: 255.x.x.x

Default Gateway: 10.1.10.x

# Visualization Setup
All virtual machines were created and managed using Oracle VirtualBox.
Each VM uses dual network adapters:
- Adapter 1: Host-only (for internal lab communication)
- Adapter 2: NAT (for internet access)



# Milestones
1. Repo + README (this step)  - completed
2. Build AD DC VM, create test users/groups - completed
3. Deploy Splunk (indexer + universal forwarder) and ingest AD logs - completed
4. Create detection searches & dashboards  
5. Wireshark scenarios (capture, analyze)  
6. Python scripts to automate routine tasks  
7. Final report + evidence + how-to guide for recruiters
<img width="945" height="831" alt="Screenshot 2025-11-03 151324" src="https://github.com/user-attachments/assets/1ba63096-1aad-4750-b3b7-8aa74fbbf6ba" />


# Deliverables
- Step-by-step docs in /docs
- Screenshots/exports of Splunk dashboards
- Capture files (.pcap) in /docs/captures (or links)
- Python scripts in /scripts
- A single PDF lab report












# Challenge & Solution
## 1. Networking
While setting up the Active Directory lab, my virtual machines (Windows Server and Windows 11) were configured with static IPs on a Host-only network (10.1.10.x subnet).
This allowed internal communication between the two VMs but no internet access for software updates or tool downloads.

### Solution
I configured Dual Adapters: Adapter 1 and 2, then attached the Host-only Adapter
Purpose: Internal lab network (10.1.10.x) and Adapter 2 attached to NAT, respectively.

I verified connectivity by pinging my server and client IP addresses to confirm they are communicating, and by pinging 8.8.8.8 and google.com to confirm DNS and internet access.

### Outcome
Both VMs (Windows Server and Windows 11) can now:

1. Communicate within the lab network (Host-only)
2. Access the internet via NAT
3. Perform AD-related downloads, Windows updates, and install security tools such as Splunk
<img width="768" height="470" alt="Screenshot 2025-11-03 151559" src="https://github.com/user-attachments/assets/7f1a982d-b9c4-4e96-b8cf-a98b8012912d" />
<img width="763" height="462" alt="Screenshot 2025-11-03 151543" src="https://github.com/user-attachments/assets/9da14290-bb32-40f1-9c22-3e64f6b760dd" />

## 2. Splunk Web
Splunk Web returned “Oops. Page not found!” when adding a local event log input on Windows Server.
Splunk Web failed to load the local event log configuration page, likely due to permissions or UI rendering issues.

### Solution
Configured Windows Event Logs manually by editing inputs.conf under
C:\Program Files\Splunk\etc\system\local\, then restarted the Splunk service to activate the inputs.
