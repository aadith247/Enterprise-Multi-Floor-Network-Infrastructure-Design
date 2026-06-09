
# 🏢 Enterprise Multi-Floor Network Design
### Cisco Packet Tracer Simulation

![Network Topology](<img width="2098" height="1152" alt="Screenshot 2026-06-09 at 11 27 08 PM" src="https://github.com/user-attachments/assets/d877cf18-b9aa-4d44-aab5-6596c05c965b" />)


> A fully functional enterprise-grade network simulation built in Cisco Packet Tracer, spanning **4 floors** with **12 VLANs**, inter-VLAN routing, redundant Layer 3 switching, and scalable wireless access — designed to reflect real-world corporate network architecture.

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Network Architecture](#-network-architecture)
- [Floor & VLAN Layout](#-floor--vlan-layout)
- [IP Addressing Scheme](#-ip-addressing-scheme)
- [Key Technologies](#-key-technologies)
- [Device Inventory](#-device-inventory)
- [Getting Started](#-getting-started)
- [Skills Demonstrated](#-skills-demonstrated)

---

## 🌐 Overview

This project simulates a complete enterprise network for a multi-department organization across 4 floors. Each floor hosts dedicated departments, isolated via VLANs for security and traffic segmentation. A core backbone of Cisco 2911 routers and 3650 Layer 3 switches provides inter-floor routing, while 2960 Layer 2 switches handle access-layer connectivity.

| Metric | Value |
|--------|-------|
| Total Floors | 4 |
| Total VLANs | 12 (VLAN 10–120) |
| Routing Protocol | Static / Inter-VLAN Routing |
| Core Switches | Cisco 3650-24PS (Layer 3) |
| Distribution Routers | Cisco 2911 |
| Access Switches | Cisco 2960-24TT |
| Wireless APs | Per department |
| Servers | DHCP, HTTP, Email |

---

## 🏗 Network Architecture

```
                    ┌─────────────────────────────────┐
                    │         CORE BACKBONE           │
                    │   2911 Floor1 ◄──► 2911 Floor2  │
                    │         ▲               ▲        │
                    │   2911 Floor3 ◄──► 2911 Floor4  │
                    └─────────────────────────────────┘
                           ▲                 ▲
              ┌────────────┘                 └────────────┐
    ┌─────────────────┐                       ┌─────────────────┐
    │  3LSW-FLOOR1/2  │                       │  3LSW-FLOOR3/4  │
    │  (Layer 3 Core) │                       │  (Layer 3 Core) │
    └─────────────────┘                       └─────────────────┘
           ▼ ▼ ▼                                    ▼ ▼ ▼
     Access Switches                           Access Switches
    (2960 per dept)                           (2960 per dept)
```

The design follows a **3-tier hierarchical model**:
- **Core Layer** — 2911 routers for inter-floor WAN links
- **Distribution Layer** — 3650 Layer 3 switches per floor cluster for inter-VLAN routing
- **Access Layer** — 2960 switches per department connecting end devices

---

## 🗺 Floor & VLAN Layout

### 🟩 Floor 1 — Corporate Services
| VLAN | Name | Subnet | Department |
|------|------|--------|------------|
| 10 | Management | 10.10.10.0/30 | IT Management |
| 20 | Research | 10.10.10.8/30 | R&D / Research |
| 30 | HR | 10.10.10.12/30 | Human Resources |

### 🟪 Floor 2 — Operations
| VLAN | Name | Subnet | Department |
|------|------|--------|------------|
| 40 | Marketing | — | Marketing |
| 50 | Accounting | — | Accounting |
| 60 | Finance | — | Finance |

### 🟦 Floor 3 — Customer & Logistics
| VLAN | Name | Subnet | Department |
|------|------|--------|------------|
| 70 | Logistics | — | Logistics |
| 80 | Guest Area | — | Guest/Visitor |
| 90 | Customer Care | — | Customer Service |

### 🟨 Floor 4 — Administration & IT Infrastructure
| VLAN | Name | Subnet | Department |
|------|------|--------|------------|
| 100 | Administration | — | Admin |
| 110 | ICT | — | ICT Department |
| 120 | Server Room | — | DHCP / HTTP / Email Servers |

---

## 📡 IP Addressing Scheme

All inter-router and inter-switch WAN links use **/30 subnets** from the `10.10.10.0/24` block, allowing exactly 2 usable host addresses per point-to-point link.

| Link | Subnet |
|------|--------|
| Floor1 Router ↔ Floor2 Router | 10.10.10.32/30 |
| Floor1 Router ↔ Floor3 Router | 10.10.10.28/30 |
| Floor1 Router ↔ Floor4 Router | 10.10.10.16/30 |
| Floor2 Router ↔ Floor3 Router | 10.10.10.40/30 |
| Floor2 Router ↔ Floor4 Router | 10.10.10.36/30 |
| Floor3 Router ↔ Floor4 Router | 10.10.10.44/30 |
| 3LSW-Floor3 ↔ Router Links | 10.10.10.48/30, 10.10.10.52/30 |
| 3LSW-Floor4 ↔ Router Links | 10.10.10.20/30, 10.10.10.24/30 |

---

## ⚙️ Key Technologies

- **VLANs & Trunking** — 802.1Q trunk links between switches; each department isolated in its own VLAN
- **Inter-VLAN Routing** — Handled by Cisco 3650 Layer 3 switches using Switched Virtual Interfaces (SVIs)
- **DHCP** — Centralized DHCP server on Floor 4 Server Room (VLAN 120) serving all VLANs via DHCP relay
- **DNS / HTTP / Email** — Dedicated servers in the Floor 4 server room
- **Wireless Access** — Each department has a dedicated Access Point for wireless connectivity
- **Point-to-Point WAN Links** — /30 subnets connecting all routers in a partial mesh topology
- **Security Segmentation** — VLAN isolation prevents unauthorized cross-department traffic

---

## 🖥 Device Inventory

| Device Type | Model | Count | Role |
|------------|-------|-------|------|
| Router | Cisco 2911 | 4 | Floor gateway / inter-floor routing |
| L3 Switch | Cisco 3650-24PS | 4 | Distribution / inter-VLAN routing |
| L2 Switch | Cisco 2960-24TT | 11 | Access layer per department |
| PC | PC-PT | 12 | End-user workstations |
| Printer | Printer-PT | 12 | Departmental printers |
| Access Point | AccessPoint-PT | 11 | Wireless per department |
| Server | Server-PT | 3 | DHCP, HTTP, Email |
| Laptop | Laptop-PT | 1 | Mobile client |

---

## 🚀 Getting Started

### Prerequisites
- [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer) 8.0 or later (free with Cisco NetAcad account)

### Running the Simulation

1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/enterprise-network-design.git
   cd enterprise-network-design
   ```

2. Open Packet Tracer and load the file:
   ```
   File → Open → Enterprise.pkt
   ```

3. Click the **Play** button (bottom-left) to start the simulation.

4. To test connectivity, open any PC's Command Prompt and run:
   ```
   ping <destination-ip>
   ```

5. Use **Simulation Mode** (bottom-right) to trace packet paths across VLANs and floors.

---

## 🎯 Skills Demonstrated

- ✅ Enterprise network design following hierarchical 3-tier model
- ✅ VLAN configuration and 802.1Q trunking
- ✅ Layer 3 switching and SVI-based inter-VLAN routing
- ✅ Subnetting with /30 point-to-point WAN links
- ✅ DHCP server configuration with relay agents
- ✅ Wireless network integration per department
- ✅ Multi-router topology with partial mesh redundancy
- ✅ Server deployment (DHCP, HTTP, Email)
- ✅ Cisco IOS CLI configuration (routers and switches)

---

## 📁 Project Files

```
enterprise-network-design/
├── Enterprise.pkt          # Cisco Packet Tracer simulation file
├── README.md               # This file
└── Screenshot_*.png        # Network topology diagram
```

---

## 📄 License

This project is open for educational and portfolio purposes. Feel free to fork, adapt, and learn from it.

---

<p align="center">Built with ❤️ using Cisco Packet Tracer</p>
