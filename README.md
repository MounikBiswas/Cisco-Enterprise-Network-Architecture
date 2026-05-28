# Cisco Networking Portfolio: Multi-Layer Enterprise Architecture

## 📌 Project Overview
This repository serves as a comprehensive log of networking labs designed and implemented using **Cisco Packet Tracer**. The project tracks a multi-stage network build, progressing from foundational device security to advanced Layer 2 segmentation and automated VLAN propagation.

---

## 🛠️ Phase 1: Basic Router & Switch Hardening
**Goal:** Establish a secure baseline for network management.

### Applied Configurations (CLI Commands):
```bash
! Entering Global Configuration
Switch> enable
Switch# configure terminal
Switch(config)# hostname Core_Switch

! Securing Passwords
Switch(config)# enable secret class
Switch(config)# service password-encryption

! Securing Lines (Console and Telnet/SSH)
Switch(config)# line con 0
Switch(config-line)# password cisco
Switch(config-line)# login
Switch(config-line)# exit
Switch(config)# line vty 0 4
Switch(config-line)# password cisco
Switch(config-line)# login
Switch(config-line)# exit

! Setting MOTD Banner
Switch(config)# banner motd # UNAUTHORIZED ACCESS PROHIBITED #


# Cisco Networking Portfolio: Multi-Layer Enterprise Architecture

## 📌 Project Overview
This repository serves as a comprehensive log of networking labs designed and implemented using **Cisco Packet Tracer**. The project tracks a multi-stage network build, progressing from foundational device security to advanced Layer 2 segmentation and automated VLAN propagation.

---

## 🛠️ Phase 1: Basic Router & Switch Hardening
**Goal:** Establish a secure baseline for network management.

### Applied Configurations (CLI Commands):
```bash
! Entering Global Configuration
Switch> enable
Switch# configure terminal
Switch(config)# hostname Core_Switch

! Securing Passwords
Switch(config)# enable secret class
Switch(config)# service password-encryption

! Securing Lines (Console and Telnet/SSH)
Switch(config)# line con 0
Switch(config-line)# password cisco
Switch(config-line)# login
Switch(config-line)# exit
Switch(config)# line vty 0 4
Switch(config-line)# password cisco
Switch(config-line)# login
Switch(config-line)# exit

! Setting MOTD Banner
Switch(config)# banner motd # UNAUTHORIZED ACCESS PROHIBITED #


📂 Phase 2: VLAN Segmentation (IT & Sales)
Goal: Logically isolate departments to improve security, prevent lateral movement, and reduce broadcast traffic.

Topology Data:
VLAN 2 (IT Dept): PC0 (10.0.0.1/8) & PC1 (10.0.0.2/8)

VLAN 3 (SALES Dept): PC2 (10.0.0.3/8) & PC3 (10.0.0.4/8)

Applied Configurations (CLI Commands):



! Creating VLANs
Switch(config)# vlan 2
Switch(config-vlan)# name IT
Switch(config-vlan)# exit
Switch(config)# vlan 3
Switch(config-vlan)# name SALES
Switch(config-vlan)# exit

! Assigning Switchports to IT
Switch(config)# interface range fastEthernet 0/1 - 2
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 2
Switch(config-if-range)# exit

! Assigning Switchports to SALES
Switch(config)# interface range fastEthernet 0/3 - 4
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 3
Switch(config-if-range)# exit



🚀 Phase 3: Enterprise VTP & Multi-Switch Management
Goal: Automate VLAN database synchronization across multiple switches using VTP (VLAN Trunking Protocol) and configure 802.1Q Trunking.

Network Architecture:
VTP Domain: XYZCompany.com

VLAN 2 (HR Dept): 192.168.10.3, 192.168.10.4, 192.168.10.7, 192.168.10.8

VLAN 3 (ACCT Dept): 192.168.10.5, 192.168.10.6, 192.168.10.9, 192.168.10.10

VLAN 4 (IT Dept): Localized to the Transparent switch.

Applied Configurations (CLI Commands):
1. VTP SERVER Configuration:

Switch(config)# vtp mode server
Switch(config)# vtp domain XYZCompany.com
Switch(config)# vlan 2
Switch(config-vlan)# name HR
Switch(config)# vlan 3
Switch(config-vlan)# name ACCT
! Configuring Trunk Link
Switch(config)# interface fastEthernet 0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 1-99
2. VTP CLIENT Configuration:
Switch(config)# vtp mode client
Switch(config)# vtp domain XYZCompany.com
! Configuring Trunk Link to receive VLANs
Switch(config)# interface fastEthernet 0/1
Switch(config-if)# switchport mode trunk

3. VTP TRANSPARENT Configuration:
Switch(config)# vtp mode transparent
Switch(config)# vtp domain XYZCompany.com
! Configuring Trunk Link to forward VTP packets
Switch(config)# interface fastEthernet 0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 1-99

🧪 Incident Logs & Connectivity Testing
Network isolation was rigorously tested using ICMP Ping packets.

Incident 1: Intra-VLAN Communication (SUCCESS)

Action: Pinging from HR PC (192.168.10.3) to HR PC (192.168.10.7) across the Trunk link.

Result: Reply from 192.168.10.7: bytes=32 time=1ms TTL=128

Status: 4/4 Packets Received (0% loss). VTP and Trunking are functioning correctly.

Incident 2: Inter-VLAN Isolation (FAILED AS INTENDED)

Action: Pinging from HR PC (192.168.10.3) to ACCT PC (192.168.10.9).

Result: Request timed out.

Status: 4/4 Packets Lost (100% loss). Layer 2 departmental security isolation is successfully verified.

📚 Knowledge Base & Methodologies
Configurations and network topologies in this repository were modeled after industry-standard routing and switching protocols, utilizing the following instructional resources:

VLAN Configuration & Routing Logic

Advanced Multi-Switch VTP Deployments                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              
