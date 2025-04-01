# network-lab-portofolio

# 🖧 Basic LAN Setup for a Small Office with Internet Access

This project simulates a simple local area network (LAN) setup for a small office with two departments: **Administration** and **Production**. Each department has its own switch and a group of PCs, all connected to a central router that provides internet access using **NAT (Network Address Translation)**.

The simulation is built using **Cisco Packet Tracer**.

---

## 🎯 Objectives

- Create a segmented LAN for two departments using two switches.
- Assign static IP addresses to all client devices.
- Connect the internal LANs to the internet through a router.
- Implement NAT on the router so internal IPs can access the internet.

---

## 🧰 Tools & Devices Used

- Cisco 2911 Router
- 2x Cisco 2960 Switches
- 6x PC-PT Clients
- 1x Server (as Internet simulation)
- Cisco Packet Tracer 8.x

---

## 🌐 Network Topology

![Network Topology](./screenshots/topologi.png)

---

- **Admin Network**: `192.168.10.0/24`
- **Production Network**: `192.168.20.0/24`
- Internet: 8.8.8.0/24

---

## 🧠 Internet Simulation in Packet Tracer

Since Cisco Packet Tracer doesn't provide real internet access, this project includes a simulated internet setup using a local server device.

### ✅ How It Works:

- A local server is assigned the IP `8.8.8.8` to mimic Google DNS.
- The router connects directly to this server using the same subnet (`8.8.8.0/24`).
- DNS service is enabled on the server with domain mappings:
  - `google.com` → `8.8.8.8`
  - `youtube.com` → `8.8.8.8`
- HTTP and HTTPS service is also enabled so clients can browse using Packet Tracer's web browser.

This allows client PCs to resolve domain names and access a mock internet environment realistically.

---

## 🧠 IP Address Plan

| Device | IP Address     | Subnet Mask     | Gateway        |
|--------|----------------|-----------------|----------------|
| PC1    | 192.168.10.2   | 255.255.255.0   | 192.168.10.1   |
| PC2    | 192.168.10.3   | 255.255.255.0   | 192.168.10.1   |
| PC3    | 192.168.10.4   | 255.255.255.0   | 192.168.10.1   |
| PC4    | 192.168.20.2   | 255.255.255.0   | 192.168.20.1   |
| PC5    | 192.168.20.3   | 255.255.255.0   | 192.168.20.1   |
| PC6    | 192.168.20.4   | 255.255.255.0   | 192.168.20.1   |

---

## 🔧 Configuration Overview

### Router (2911)

- Interface G0/0 → Internet (`8.8.8.1`)
- Interface G0/1 → Admin LAN (`192.168.10.1`)
- Interface G0/2 → Production LAN (`192.168.20.1`)
- NAT configured for both internal networks

### Switches (2960)

- Access ports for PCs
- Connection to the router via Fa0/1

### PCs

- Static IPs set manually
- Default gateway points to router interface

---

## 🔧 Configuration Files

All device configurations are available in the [`config/`](./config) folder.

| Device   | File                          |
|----------|-------------------------------|
| Router   | `config/router-config.txt`    |
| Switch 1 | `config/switch-admin.txt`     |
| Switch 2 | `config/switch-production.txt`|
| PCs      | Manual IP setup (see [IP Plan](#-ip-address-plan)) |

Each configuration includes:
- Interface setup
- NAT and IP assignment
- VLANs (if applicable)
- Any additional settings per project scope

---

## ✅ Testing Checklist

| Test                                  | Result |
|---------------------------------------|--------|
| PC1 ↔ PC2 (Admin LAN)                 | ✅     |
| PC4 ↔ PC5 (Production LAN)            | ✅     |
| PC1 ↔ PC4 (Cross-network communication)| ✅    |
| Internet access from PC1 / PC4        | ✅     |

---

## 📸 Testing Evidence

All testing steps are documented with screenshots in the [`screenshots/`](./screenshots) folder.

Example:

- `ping_pc1_pc2.png` → Ping between Admin PCs
- `ping_pc4_pc5.png` → Ping between Production PCs
- `ping_pc1_pc4.png` → Ping cross-network
- `ping_pc1_google.png` → Internet access via NAT

---

## 🧩 Troubleshooting Tips

| Issue                           | Solution                            |
|----------------------------------|-------------------------------------|
| No internet access               | Check NAT configuration             |
| No ping between PCs              | Check cable type, interface status  |
| No default gateway               | Ensure PCs have the correct gateway |

---

## 📦 Project Files

You can download and open the full simulation in [Cisco Packet Tracer](https://www.netacad.com/):

- [`packet-tracer/basic-lan-final-config.pkz`](./packet-tracer/basic-lan-final-config.pkz)

**Contents:**
- Fully configured router, switches, and PCs
- NAT and IP settings
- Cloud internet access simulation

Open with Cisco Packet Tracer 8.x or later.

---

## 📎 Notes

- This project is the foundation for upcoming versions:
  - VLAN segmentation
  - DHCP automation
  - Access Control Lists (ACL)
  - Network Monitoring (SNMP/Nagios)

---

## 📚 References

- [Cisco Packet Tracer - NetAcad](https://www.netacad.com/)
- [Cisco NAT Configuration Guide](https://www.cisco.com/c/en/us/support/docs/ip/network-address-translation-nat/13772-12.html)

