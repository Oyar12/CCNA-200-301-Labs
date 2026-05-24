# CCNA 200-301 – Day 12 Lab: The Life of a Packet

## 1. Theory Overview

### ARP – Address Resolution Protocol

- **Purpose:** ARP resolves an IP address to a MAC address within a local network segment.
- **Process:**  
  - **ARP Request:** Broadcast – asks “Who has this IP?”
  - **ARP Reply:** Unicast – the owner of the IP replies with its MAC address.
- **Packet Journey:**  
  - When a packet traverses a routed network, **the MAC address is updated at each hop**, but the **IP addresses remain unchanged** from source to destination.

### CIDR – Classless Inter Domain Routing

- CIDR allows network segmentation without class restrictions (removes classful requirements: no strict /8, /16, /24).
- This enables large networks to be split into smaller, more efficient subnets ("subnetworks" or "subnets"), maximizing address utilization.

---

## 2. Lab Scenario

This lab explores how packets, including their source and destination MAC addresses, travel through a multi-router network.

**Objectives:**
- Analyze the step-by-step path of a packet from PC1 to various destinations (PC3, PC4).
- Identify Source and Destination MAC addresses at each hop and segment in the route.
- Gain hands-on experience with ARP behavior and MAC address changes across routers and switches.

**Topology Overview:**  
Multiple PCs are connected through two switches and three routers. Key challenges focus on the layer 2 (MAC) and layer 3 (IP) addressing of packets during their journey.

---

## 3. Lab Tasks

**Example Exercise:**
1. PC1 pings PC4.
    - For every segment in the path from PC1 to PC4, identify:
        - Source/Destination MAC addresses for each device/interface (e.g., R1 G0/0).
        - MAC address learning order (before simulation, use ping to force ARP).
    - Use CLI and simulation mode for packet analysis.

2. Repeat the analysis for PC1 to PC3 and PC4 to PC1.

**Sample Expected Answers:**
- On each link, the source MAC is the sender’s interface, destination MAC is the receiver’s interface.
- The output may look like:  
  - Source: `000D.BA11.1111`, Dest: `000D.01AA.AAAA` (exact addresses will depend on lab config).

---

## 4. Key Insights & Troubleshooting

- **MAC Address Changes:**  
  At every hop (router, switch), the MAC address changes according to the outgoing and incoming interfaces, but the IP addresses **remain constant** end-to-end.
- **Correct ARP Process:**  
  If ping fails, verify ARP tables and ensure ARP process has completed (use simulation mode and observe ARP packets).
- **Good Practice:**  
  Always initiate a ping first to populate ARP tables before diving into simulation analysis.

---

## 5. Handwritten Notes

See the example below for theory reminders and subnetting explanations:

<!-- Add your handwritten notes image here, e.g. ![Handwritten notes](image5) -->

---

## 6. Screenshots

<img width="576" height="1280" alt="WhatsApp Image 2026-05-24 a16 37 38" src="https://github.com/user-attachments/assets/0a75df23-a455-4dcc-ba3a-d76ec021d2c1" />
<img width="1918" height="1008" alt="Screenshot 2026-05-21 062701" src="https://github.com/user-attachments/assets/c5a67508-d1e7-4872-bbbc-264eccc55614" />

---

## Author

Lab and documentation by **Oyar12**, based on Cisco Packet Tracer CCNA 200-301 curriculum.
