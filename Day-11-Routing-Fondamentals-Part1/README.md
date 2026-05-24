# CCNA Day 11 (Part 1) - Routing Fundamentals & Static Routing

This repository contains the theoretical core concepts and practical lab documentation for **Day 11 (Part 1)** of the CCNA 200-301 curriculum (Jeremy's IT Lab). This section covers router forwarding behavior, routing table logic, and static route implementation.

---

## 📘 1. Routing Fundamentals

Layer 3 routers forward packets based on **Destination IP addresses**, fundamentally differing from Layer 2 switches which forward frames based on Destination MAC addresses.

### 🔄 Router vs. Switch Behavior (Unknown Destinations)


| Feature | L2 Switch Behavior | L3 Router Behavior |
| :--- | :--- | :--- |
| **Unknown Destination** | **Floods** the frame out of all ports (except the ingress port). | **Drops** the packet immediately. |
| **Exception** | None. | Will not drop the packet if a **Gateway of Last Resort** (Default Route) is configured. |

### 🧠 The Routing Table & Matching Logic

When a router processes a packet, it compares the destination IP address against entries in its routing table (`show ip route`) using the following strict hierarchy:

#### 1. Longest Prefix Match (Most Specific Route)
If multiple entries match the destination IP address, the router always selects the route with the **longest prefix length** (highest CIDR notation).

> 💡 **Visual Example:**
> A packet is destined for `192.168.1.1`. The routing table contains:
> * `192.168.0.0/16` (Matches, but length is 16)
> * `192.168.1.0/24` (Matches, length is 24)
> 
> **Decision:** The router selects **`192.168.1.0/24`** because it is the most specific match.

#### 2. Administrative Distance (AD)
If the prefix lengths are identical, the router compares the trustworthiness of the routing sources. Lower AD is preferred (e.g., Static route $AD = 1$ vs. OSPF $AD = 110$).

#### 3. Metric
If both the prefix length and AD are identical, the router uses the route with the lowest metric (cost).

---

## 🛠 2. Static Routing Configuration

Static routes are manually defined by the administrator. They provide precise control and low CPU overhead, making them ideal for small, stable environments or stub networks.

### ⚙️ Command Syntax

To configure a static route, execute one of the following commands in **global configuration mode**:

**Option A: Next-Hop IP Address (Recommended for multi-access links like Ethernet)**
```ios
Router(config)# ip route <destination-network> <subnet-mask> <next-hop-ip-address>
```

**Option B: Exit Interface (Recommended for point-to-point serial links)**
```ios
Router(config)# ip route <destination-network> <subnet-mask> <exit-interface>
```

### 🌐 Default Route (Gateway of Last Resort)

A default route matches all traffic regardless of the destination. It acts as a safety net to forward traffic toward the Internet or an upstream provider when no specific route exists.

```ios
Router(config)# ip route 0.0.0.0 0.0.0.0 <next-hop-ip-address>
```

---

## 🧪 3. Practical Lab Guide

### 🎯 Objective
Establish flawless, bidirectional reachability between isolated subnets separated by multiple intermediary routers (e.g., ensuring `PC1` can successfully ping `PC2` and receive the reply).

### 🔍 Verification & Troubleshooting Commands

Use these essential diagnostic tools to verify configurations and isolate path failures:

* `show ip route` — Displays the active IP routing table matrix and the Gateway of Last Resort.
* `show ip interface brief` — Verifies the physical/logical operational status (`Up/Up`) and IP assignments of all ports.
* `ping <ip-address>` — Tests end-to-end network layer connectivity.
* `traceroute <ip-address>` — Tracks the step-by-step hop path packets take to reach their destination, isolating where a drop occurs.

### ⚠️ Key Troubleshooting Takeaways

* **Two-Way Reachability is Mandatory:** A network path is a round trip. For a `ping` to succeed, the packet must reach the destination **and** the destination must know the path back to the source. If any router along either path lacks a return route, communication fails.
* **IP Address Overwriting:** In Cisco IOS, assigning a new IP address to an interface automatically overwrites the old one. There is no need to manually delete (`no ip address`) the existing configuration first.

---
_Notes and lab configurations are aligned with Jeremy's IT Lab CCNA Complete Course._
