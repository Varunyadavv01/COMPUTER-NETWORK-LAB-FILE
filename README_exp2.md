# ENCS304 – Computer Networks
# Experiment 2: Packet Flow Visualization Using Simulation Mode

**Name:** Puneet Kumar Gupta
**Roll No.:** 2301010171
**Programme:** B.Tech Computer Science & Engineering
**Section:** C

---

## Overview

This experiment uses Cisco Packet Tracer's **Simulation Mode** to observe how packets travel through a small Local Area Network (LAN). We trace ARP and ICMP traffic and study how a switch learns MAC addresses from live traffic.

---

## Network Topology

```
  PC0 (192.168.20.1)  ----+
                          |
  PC1 (192.168.20.2)  ----+---  Switch0 (2960)
                          |
  PC2 (192.168.20.3)  ----+
```

| Device  | Interface    | IP Address    | Subnet Mask     |
|---------|-------------|---------------|-----------------|
| PC0     | Fa0          | 192.168.20.1  | 255.255.255.0   |
| PC1     | Fa0          | 192.168.20.2  | 255.255.255.0   |
| PC2     | Fa0          | 192.168.20.3  | 255.255.255.0   |
| Switch0 | Fa0/1 → PC0  | —             | —               |
| Switch0 | Fa0/2 → PC1  | —             | —               |
| Switch0 | Fa0/3 → PC2  | —             | —               |

---

## Tasks Completed

### Task 1 – Build a Simple LAN
- Added 1 Cisco 2960 switch and 3 PCs
- Assigned IP addresses 192.168.20.1, .2, and .3 with subnet /24
- Connected all PCs to the switch using Copper Straight-Through cables

### Task 2 – First Ping Observation (PC0 → PC1)
- Enabled Simulation Mode
- Entered `ping 192.168.20.2` on PC0's Command Prompt
- Observed the full ARP Request → ARP Reply sequence before ICMP
- Switch flooded ARP broadcast to all ports (PC1 and PC2 received it)
- PC1 replied with unicast ARP Reply; switch learned both MAC addresses
- ICMP Echo Request and Reply then followed successfully

### Task 3 – Second Ping Observation (PC0 → PC1)
- Pinged 192.168.20.2 again from PC0
- ARP cache was already populated — no ARP events in the event list
- Only ICMP Echo Request and Reply appeared (~5 events vs ~11 before)
- Switch used its MAC table directly; no flooding occurred

### Task 4 – MAC Table Verification
- Opened Switch0 CLI and ran `show mac address-table`
- Confirmed PC0 and PC1 MAC addresses appeared as DYNAMIC entries on Fa0/1 and Fa0/2
- PC2 MAC was absent (no traffic sent/received by PC2)

---

## Key Observations

| Aspect                   | First Ping         | Second Ping        |
|--------------------------|--------------------|--------------------|
| ARP broadcast sent?      | Yes                | No (cached)        |
| Total simulation events  | ~11                | ~5                 |
| Switch flooding?         | Yes                | No                 |
| Packets received by PC2? | Yes (ARP flood)    | No                 |
| Round-trip time          | Slower             | Faster             |

---

## Files Submitted

| File                  | Description                                      |
|-----------------------|--------------------------------------------------|
| `exp2_packetflow.pkt` | Cisco Packet Tracer simulation file              |
| `output_exp2.txt`     | Full event log and observations for all tasks    |
| `report_exp2.pdf`     | Detailed report with diagrams and explanations   |
| `README.md`           | This file                                        |

---

## Concepts Demonstrated

- **ARP (Address Resolution Protocol):** Maps IP addresses to MAC addresses before communication begins.
- **ICMP (Ping):** Tests reachability between hosts at the network layer.
- **Switch MAC Learning:** Switches learn source MAC addresses from incoming frames and build a MAC address table dynamically.
- **Broadcast vs Unicast:** ARP uses broadcast (first ping); subsequent traffic is unicast once MACs are known.

---

## How to Run the Simulation

1. Open `exp2_packetflow.pkt` in Cisco Packet Tracer (v7.x or later).
2. Switch to **Simulation Mode** (clock icon, bottom right).
3. Filter events to show **ARP** and **ICMP** only.
4. Click on PC0 → Desktop → Command Prompt → type `ping 192.168.20.2`.
5. Press **Play** or use **Step** (single-step forward) to watch each packet move.
6. After the first ping completes, ping again and compare the event count.
7. Open Switch0 → CLI → type `show mac address-table` to confirm MAC learning.

---

*Submitted as part of Assignment 2 | ENCS304 Computer Networks*
