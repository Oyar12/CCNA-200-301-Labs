# CCNA Day 8 - IPv4 Addressing (Part 2): Lecture & Lab

This repository contains the theoretical notes and technical documentation for the practical lab associated with **Day 8** of the CCNA curriculum.

---

## 📘 1. Lecture Notes (Theory)

### A. Maximum Hosts per Network
To determine the number of assignable IP addresses for hosts (PCs, routers, servers) within a network or subnet, use the following formula:

$$\text{Maximum Hosts} = 2^n - 2$$

* **$n$**: Number of bits reserved for the host portion (*host bits*).
* **Why $- 2$ ?**
  1. We subtract the first address (where all host bits are `0`), which represents the **Network ID**.
  2. We subtract the last address (where all host bits are `1`), which represents the **Broadcast Address**.

**Application Example:**
For the network `192.168.1.0/24`:
* The `/24` mask means 24 bits are for the network and $32 - 24 = 8$ bits are for the hosts ($n = 8$).
* Total host combinations: $2^8 = 256$.
* Usable hosts: $2^8 - 2 = 254$ valid addresses (from `.1` to `.254`).

### B. Analyzing the `show ip interface brief` Command
This fundamental command verifies the status of a Cisco device's interfaces. The two status columns correspond to the OSI model layers:

1. **Status (Layer 1 - Physical):** Indicates if the cable is plugged in and functional, or if the interface is manually shut down (`administratively down`).
2. **Protocol (Layer 2 - Data Link):** Indicates if the encapsulation and link-layer protocol (like Ethernet) are operational.

> **Note:** For an interface to be fully functional, it must display an **Up / Up** status.

---

## 🛠 2. Practical Lab Guide

### A. Topology Overview
The lab is built using **Cisco Packet Tracer** and implements inter-vlan routing through a central router interconnecting three distinct network architectures:

* **Local Area Network 1 (Blue LAN):** Subnet `15.0.0.0/8`
  * Gateway (R1 G0/0): `15.255.255.254`
  * End Host (PC1): `15.0.0.1`
* **Local Area Network 2 (Green LAN):** Subnet `182.98.0.0/16`
  * Gateway (R1 G0/1): `182.98.255.254`
  * End Host (PC2): `182.98.0.1`
* **Local Area Network 3 (Yellow LAN):** Subnet `201.191.20.0/24`
  * Gateway (R1 G0/2): `201.191.20.254`
  * End Host (PC3): `201.191.20.1`

### B. R1 Configuration Script
Below are the commands applied via the router CLI to configure the interfaces and document the topology:

```ios
# Enter privileged EXEC and global configuration mode
Router> enable
Router# configure terminal
Router(config)# hostname R1

# Configure GigabitEthernet 0/0 interface (LAN 1)
R1(config)# interface gigabitethernet 0/0
R1(config-if)# ip address 15.255.255.254 255.0.0.0
R1(config-if)# description to SW1
R1(config-if)# no shutdown
R1(config-if)# exit

# Configure GigabitEthernet 0/1 interface (LAN 2)
R1(config)# interface g0/1
R1(config-if)# ip address 182.98.255.254 255.255.0.0
R1(config-if)# description to SW2
R1(config-if)# no shutdown
R1(config-if)# exit

# Configure GigabitEthernet 0/2 interface (LAN 3)
R1(config)# interface g0/2
R1(config-if)# ip address 201.191.20.254 255.255.255.0
R1(config-if)# description to SW3
R1(config-if)# no shutdown
R1(config-if)# exit

# Save the running configuration
R1(config-if)# do write memory
```

### C. Verification Commands
The following diagnostic commands were executed to validate the router status:

**Brief verification of IP addresses and status:**
```ios
R1# show ip interface brief
```
* **Expected Result:** `GigabitEthernet0/0`, `0/1`, and `0/2` interfaces must display status `up` and protocol `up`.

**Verification of interface descriptions:**
```ios
R1# show interfaces description
```
* **Expected Result:** Confirms that each interface is properly documented pointing to its respective switch (`to SW1`, `to SW2`, `to SW3`).

---

## 📸 3. Validation and Results

### Host Configuration
The IP addresses for PC1, PC2, and PC3 were statically assigned in Packet Tracer (`Desktop > IP Configuration`). The router IP address was specified as the **Default Gateway**.

### Connectivity Tests (Ping)
ICMP requests were sent from the PC1 command prompt to the other subnets:
* `ping 182.98.0.1` (PC2) ➡️ **Success** (The first packet may time out during ARP resolution, then subsequent packets reply with a TTL of 127).
* `ping 201.191.20.1` (PC3) ➡️ **Success**.

Routing between the three subnets is fully operational.

<img width="1920" height="1080" alt="Screenshot_20260519_220325" src="https://github.com" />
<img width="1920" height="1080" alt="Screenshot_20260519_220218" src="https://github.com" />
<img width="1920" height="1080" alt="Screenshot_20260519_220024" src="https://github.com" />
<img width="576" height="1280" alt="jpeg" src="https://github.com" />
<img width="1920" height="1080" alt="Screenshot_20260519_220024" src="https://github.com" />
