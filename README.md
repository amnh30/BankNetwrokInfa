# Network Infrastructure Documentation

## Overview
This repository contains the network architecture, configurations, and device details for a structured enterprise network. It includes VLAN segmentation, OSPF routing, and security configurations.

## Key Components of the Network Diagram

### 1. Core Network (Central Area - Yellow Box)
- Implements OSPF (Open Shortest Path First) routing.
- Comprises multiple interconnected routers and switches.
- Facilitates communication between various VLANs.

### 2. Departmental VLANs (Left and Right Sections)
**Left Side VLANs:**
- Management
- Research
- HR
- Marketing
- Accounts
- Finance

**Right Side VLANs:**
- Logistics
- Customer
- Guest
- Admin
- ICT
- Servers Room

### 3. Network Devices
- **12** Access Points (APs) for wireless connectivity
- **12** PCs for employees
- **12** Printers for document processing
- **12** IP Phones
- **12** Switches
- **4** Multilayer Switches
- **4** Routers

### 4. Connections Between Core and VLANs
- The core network is connected to VLANs using **Gigabit Ethernet (Gig) connections**.
- **Dotted and solid lines** indicate physical and logical connections.

---

## Naming Conventions
Each device follows a structured naming pattern:
**Format:** `FF_M_A`
- `FF`: Floor Number
- `M`: Department or Section
- `A`: Device Name

### Abbreviations
#### Floors:
- **FF** - First Floor
- **SF** - Second Floor
- **TF** - Third Floor
- **FourF** - Fourth Floor

#### Departments:
- **M** - Management
- **R** - Research
- **HR** - HR
- **Mar** - Marketing
- **A** - Accounts
- **F** - Finance
- **L** - Logistics
- **C** - Customer
- **G** - Guest
- **Admin** - Admin
- **ICT** - ICT
- **Servers** - Servers Room

#### Devices:
- **PC** - Personal Computer
- **A** - Access Point
- **IPP** - IP Phone
- **S** - Switch
- **Pr** - Printer

---

## Network Configurations
### Switch Configuration
```bash
enable
configure terminal
hostname Router4

# Console Access
line console 0
password cisco
login
exit

# Remote Access (Telnet/SSH)
line vty 0 4
password cisco
login
exit

# Message of the Day (MOTD) Banner
banner motd #
*******************************************
* WARNING: Unauthorized access is prohibited! *
* This system is for authorized users only.   *
* All activities are logged and monitored.    *
*******************************************
#

no ip domain-lookup
service password-encryption
do wr
```

### VLAN Configuration on Switch
```bash
enable
configure terminal

# Configure trunk interfaces
int range fa0/1-2
switchport mode trunk
exit

# Create VLAN 40
vlan 40
name Fourth_Floor
exit

# Configure Access Ports
int range fa0/3-24
switchport mode access
switchport access vlan 40
switchport port-security
switchport port-security maximum 2
switchport port-security mac-address sticky
switchport port-security violation shutdown
exit
do wr
```

### Multilayer Switch Configuration
```bash
enable
configure terminal

# Console Access
line console 0
password cisco
login
exit

# SSH Settings
ip domain-name cisco.net
username cisco password cisco
crypto key generate rsa
1024

# Remote Access (SSH only)
line vty 0 15
login local
transport input ssh
exit

# Security Configurations
no ip domain-lookup
enable password cisco
service password-encryption
do wr

# VLAN 10 Configuration
interface range fa0/1 - 24
switchport mode access
switchport access vlan 10
exit
do wr
```

## Repository Structure
```
📂 Network-Documentation
 ├── 📁 Configurations
 │   ├── router_config.txt
 │   ├── switch_config.txt
 │   ├── vlan_config.txt
 ├── 📁 Diagrams
 │   ├── network_topology.png
 │   ├── vlan_structure.png
 ├── README.md
```

## License
This project is licensed under the MIT License. See the LICENSE file for details.

## Contact
For queries, reach out via [amn951753@gmail.com](mailto:amn951753@gmail.com).