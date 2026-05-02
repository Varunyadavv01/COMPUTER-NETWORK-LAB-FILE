# ENCS304 – Computer Networks
## Assignment 1: Basic Network Topologies Using Switches and Hubs

**Name:** Puneet Kumar Gupta
**Roll No.:** 2301010171
**Programme:** B.Tech Computer Science & Engineering
**Section:** C
**Date:** 27 February 2026

---

## 📁 Submission Files

| File | Description |
|------|-------------|
| `exp1_topologies.pkt` | Cisco Packet Tracer simulation file containing all four topology experiments |
| `output_exp1.txt` | Ping results and observations for all tasks |
| `report_exp1.pdf` | Full report with topology screenshots, ping results, and conclusions |
| `README.md` | This file — instructions on how to open and test the simulation |

---

## 🛠️ Requirements

- **Cisco Packet Tracer** version 8.0 or later (recommended)
  - Download from [Cisco NetAcad](https://www.netacad.com) (free account required)
- No additional software or hardware required — the simulation runs entirely within Packet Tracer

---

## 🚀 How to Open the Simulation

1. Install and launch **Cisco Packet Tracer**
2. Go to **File → Open** (or press `Ctrl + O`)
3. Navigate to the folder containing the submission files
4. Select **`exp1_topologies.pkt`** and click **Open**
5. The workspace will load with all four topology experiments arranged on the canvas

> **Tip:** Each topology is labelled on the canvas (Task 1, Task 2, Task 3, Task 4) for easy identification.

---

## 🔬 How to Test Each Topology

### Task 1 – Star Topology (Switch)
- **Devices:** Switch1 (2960-24TT) + PC0, PC1, PC2, PC3
- **Subnet:** `192.168.10.0/24`
- **To test:**
  1. Click on **PC0** → go to **Desktop** tab → open **Command Prompt**
  2. Run: `ping 192.168.10.2` (PC1), `ping 192.168.10.3` (PC2), `ping 192.168.10.4` (PC3)
  3. Observe that after the first ping (which may flood), subsequent pings are directed only to the target device

### Task 2 – Star Topology (Hub)
- **Devices:** Hub0 (Hub-PT) + PC0, PC1, PC2, PC3
- **Subnet:** `192.168.10.0/24`
- **To test:**
  1. Click on **PC0** → **Desktop** → **Command Prompt**
  2. Run: `ping 192.168.10.6`, `ping 192.168.10.7`, `ping 192.168.10.8`
  3. Switch to **Simulation Mode** (bottom-right) and press **Play** to visually observe the hub broadcasting frames to all ports on every transmission

> **Observation to note:** Unlike the switch in Task 1, the hub broadcasts every frame to all connected devices — including on repeat pings. Use Simulation Mode to see this clearly.

### Task 3 – Ring-like Topology (Switch Loop with STP)
- **Devices:** Switch0, Switch1, Switch2 (2960-24TT) + PC0–PC5 distributed across switches
- **Subnet:** `192.168.10.0/24`
- **To test:**
  1. Click on **PC0** → **Desktop** → **Command Prompt**
  2. Run: `ping 192.168.10.217` and `ping 192.168.10.218`
  3. Notice the **dashed lines** between switches — these are links blocked by STP to prevent loops
  4. Observe that traffic flows only through the STP-selected active paths

### Task 4 – Failure Test (Ring Topology)
- **Setup:** Same ring topology as Task 3
- **To test:**
  1. First confirm connectivity: ping between two PCs on different switches
  2. Hover over one of the **active (solid) inter-switch links** and click on it
  3. Select **Delete** or right-click → **Delete** to disconnect the link (simulating a failure)
  4. Wait a few seconds for **STP to recalculate** the topology (the previously blocked port will become active)
  5. Repeat the ping — communication should be restored through the alternate path with zero packet loss

> **Note:** STP convergence may take 5–15 seconds (or faster in Packet Tracer with PortFast). If the first ping times out, wait briefly and try again.

---

## 📊 IP Address Reference

### Task 1 (Switch Topology)
| Device | IP Address | Subnet Mask |
|--------|-----------|-------------|
| PC0 | 192.168.10.1 | 255.255.255.0 |
| PC1 | 192.168.10.2 | 255.255.255.0 |
| PC2 | 192.168.10.3 | 255.255.255.0 |
| PC3 | 192.168.10.4 | 255.255.255.0 |

### Task 2 (Hub Topology)
| Device | IP Address | Subnet Mask |
|--------|-----------|-------------|
| PC0 | 192.168.10.5 | 255.255.255.0 |
| PC1 | 192.168.10.6 | 255.255.255.0 |
| PC2 | 192.168.10.7 | 255.255.255.0 |
| PC3 | 192.168.10.8 | 255.255.255.0 |

### Task 3 (Ring-like Topology with STP)
| Device | IP Address | Subnet Mask |
|--------|-----------|-------------|
| PC0 | 192.168.10.210 | 255.255.255.0 |
| PC1 | 192.168.10.211 | 255.255.255.0 |
| PC2 | 192.168.10.212 | 255.255.255.0 |
| PC3 | 192.168.10.213 | 255.255.255.0 |
| PC4 | 192.168.10.214 | 255.255.255.0 |
| PC5 | 192.168.10.215 | 255.255.255.0 |

### Task 4 (Failure Test)
| Device | IP Address | Subnet Mask |
|--------|-----------|-------------|
| PC0 | 192.168.10.214 | 255.255.255.0 |
| PC1 | 192.168.10.215 | 255.255.255.0 |
| PC2 | 192.168.10.216 | 255.255.255.0 |
| PC3 | 192.168.10.217 | 255.255.255.0 |
| PC4 | 192.168.10.218 | 255.255.255.0 |
| PC5 | 192.168.10.219 | 255.255.255.0 |

---

## 💡 Key Concepts Demonstrated

- **Switch vs Hub behaviour:** Both broadcast on the first frame (unknown destination). A switch then learns MAC addresses and delivers subsequent frames only to the intended port. A hub always broadcasts to all ports, every time.
- **Spanning Tree Protocol (STP):** Automatically blocks redundant links to prevent loops and broadcast storms, while keeping backup paths available for fault recovery.
- **Fault Tolerance:** The ring topology with STP can recover from a single link failure by activating a previously blocked path, unlike a star topology where a single link failure isolates that device permanently.

---

## 📄 Viewing the Report

Open `report_exp1.pdf` with any standard PDF viewer (Adobe Acrobat, browser, etc.) to see the full topology screenshots, ping output, and analysis for all four tasks.
