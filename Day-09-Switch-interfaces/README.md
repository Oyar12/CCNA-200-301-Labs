# CCNA Day 9 - Switch Interfaces: Lecture & Lab

This repository contains the theoretical notes and technical documentation for the practical lab associated with **Day 9** of the CCNA curriculum (Jeremy's IT Lab), focusing on switch interface configuration, speed/duplex negotiation, and error management.

---

## 📘 1. Lecture Notes (Theory)

### A. Collision Domains and CSMA/CD
* **LAN Hub:** All devices connected to a hub belong to a single collision domain. Two devices cannot transmit a packet at the exact same time.
* **CSMA/CD (Carrier Sense Multiple Access with Collision Detection):**
  * **Listening:** Devices listen to the medium before transmitting to ensure it is free.
  * **Collision:** If two devices transmit simultaneously, they send out a *jamming signal*.
  * **Backoff:** Each device waits for a random period of time before attempting to retransmit.

### B. Duplex Mode (Half vs Full)
* **Half Duplex:** Two-way directional communication but not simultaneous. A device cannot send and receive data at the same time (typical for hubs).
* **Full Duplex:** Simultaneous two-way directional communication. A device can send and receive data at the same time (typical for switches).

### C. Speed and Auto-Negotiation
* **Default Settings:** Interfaces generally use `speed auto` and `duplex auto` to negotiate the best possible performance parameters with the neighboring device.
* **Duplex Mismatch:** If one side is manually configured to Full Duplex and the other side auto-negotiates to Half Duplex, severe collisions and massive performance drops will occur on the link.

### D. Interface Errors
The `show interfaces` command allows you to analyze various interface error counters:
* **Runts:** Frames that are smaller than the minimum allowed Ethernet size (64 bytes).
* **Giants:** Frames that are larger than the maximum allowed Ethernet size (1518 bytes).
* **CRC:** Frames that failed the integrity check in the FCS trailer.
* **Frame:** Frames received with an incorrect or incomplete format.
* **Input errors:** The total count of all various errors encountered on input.
* **Output errors:** The number of frames that the switch failed to transmit.

---

## 🛠 2. Practical Lab Guide

### A. Topology Overview
The entire network is configured using the **`172.16.0.0/16`** address space.

* **Router R1:** Default gateway configured with the IP address `172.16.255.254`.
* **Switch 1 (SW1):** Connected to R1 via `G0/1`, to PC1 (`172.16.0.1`) via `F0/1`, and to PC2 (`172.16.0.2`) via `F0/2`.
* **Switch 2 (SW2):** Connected to R1 via `G0/2`, to PC3 (`172.16.0.3`) via `F0/1`, and to PC4 (`172.16.0.4`) via `F0/2`.

### B. SW1 Configuration
Below are the commands applied to switch SW1 to force the uplink parameters and secure the architecture:

```ios
SW1> enable
SW1# configure terminal

# Configure the GigabitEthernet port connected to router R1
SW1(config)# interface g0/1
SW1(config-if)# speed 1000
SW1(config-if)# duplex full
SW1(config-if)# description ## to R1 ##
SW1(config-if)# exit

# Bulk disable unused ports for security purposes
SW1(config)# interface range g0/2 , f0/3 - 22
SW1(config-if-range)# shutdown
SW1(config-if-range)# end

# Save the configuration
SW1# write memory
```

> **Configuration Note:** Forcing speed and duplex manually helps prevent link downtime caused by auto-negotiation failures. Using the `interface range` command optimizes the deployment of security baseline configurations.

### C. Host Configuration (Example: PC4)
* **IP Address:** `172.16.0.4`
* **Subnet Mask:** `255.255.0.0`
* **Default Gateway:** `172.16.255.254`

### D. Verification Commands
To validate the operational status and health of the switches, use the following diagnostic commands:

* `show interface status`: Displays a clean, summary table (Status, VLAN, operational Duplex, operational Speed).
* `show interfaces f0/1`: Displays detailed technical counters for a specific interface, including the factory MAC address (BIA) and interface errors.
* `show ip interface brief`: Provides a quick overview of the logical and physical status (`Up/Up`) of all ports.
