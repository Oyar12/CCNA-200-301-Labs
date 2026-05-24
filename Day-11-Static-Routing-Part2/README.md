# Day 11 Lab: Static Routing (Part 2)

## 1. Theory Reminder

### Default Route

- The **default route** (`0.0.0.0/0`) is used to forward packets destined for unknown networks.
- Syntax:
  ```shell
  ip route 0.0.0.0 0.0.0.0 [next-hop IP or exit interface]
  ```
- Purpose: Ensures packets are forwarded to a gateway of last resort, usually an edge router.

### Static Routing

- **Static routes** are manually specified paths to reach specific networks.
- Syntax:
  ```shell
  ip route [destination_network] [subnet_mask] [next-hop IP or exit interface]
  ```

---

## 2. Lab Scenario

You are tasked with enabling end-to-end connectivity between PC1 and PC2 across a network of three routers using only static routes. The diagram below shows the required topology and addressing plan.

<!-- Add image1 (Topology) here -->

---

## 3. Professional Lab Procedure

### 3.1. Device and Address Configuration

- Assign the correct IP addresses to all router interfaces per the diagram.
- Assign each PC an IP within its subnet and specify the correct default gateway.
- No switch configuration is required.

### 3.2. Static Route Configuration

- On each router, add static routes to reach all remote networks.
- Configure the default route if a router is intended to reach destinations outside its known subnets.

### 3.3. Verification

- Test with `ping` from PC1 to PC2.
- Use `show ip route` on each router to confirm the routes are correctly installed.

---

## 4. Troubleshooting & Real Lab Results

During implementation, typical errors can occur. In a real-world professional environment, addressing misconfigurations quickly is crucial:

- **Incorrect Interface or IP Assignment:**  
  A wrong IP on a router interface will prevent connectivity. Double-check all interface settings.
- **Static Route Errors:**  
  - Wrong next-hop IP: Ensure each static route points to a valid, reachable neighbor.
  - Wrong subnet/mask: Verify all destination network and mask entries.
- **Missing or Wrong Default Route:**  
  Some routers may require a default route to handle unknown destinations.

> In this lab, each router has an intentional configuration error for troubleshooting practice.  
> Lab is considered **successful only when PC1 can ping PC2**.

**Typical Troubleshooting Methods:**
- `show ip interface brief` — check interface status and IPs.
- `show ip route` — verify routing table accuracy.
- `ping` and `traceroute` (where supported) — test end-to-end paths.
- Console error messages — address any “Invalid input detected” or unreachable gateway errors.

### Example Corrections Observed

- Fixed wrong IP on R3 interface (was `192.168.2.3.3`, set to `192.168.13.3`)
- Corrected static route for `192.168.3.0/24` on R2 (should point to `192.168.13.3`)
- Repaired static route for `192.168.12.3` on R1 (should point to `192.168.12.2`)

---

## 5. Example Key Commands

```shell
ip route 192.168.3.0 255.255.255.0 192.168.13.3
ip route 0.0.0.0 0.0.0.0 192.168.13.2
```

---

## 6. Documentation & Evidence

Attach all relevant screenshots and handwritten notes showing:

- The initial topology & addressing table
- Configuration commands entered
- Routing tables and ping results before/after corrections
- Your handwritten summary for theory and configuration

<!-- Add your images below. Example: -->
<!-- ![Lab Topology](image1)
![Initial troubleshooting](image2)
![Handwritten notes](image3) -->

---

## Author

Lab and documentation by **Oyar12**, based on Cisco Packet Tracer CCNA 200-301 curriculum.
<img width="576" height="1280" alt="WhatsApp Image 2026-0-24 at 1 37 37" src="https://github.com/user-attachments/assets/98574f01-4388-49cd-9925-00cbaef2b811" />
<img width="1920" height="1080" alt="Screenshot_20260520_153137" src="https://github.com/user-attachments/assets/0811cd7b-e7a1-411e-992e-45423c5f7d6f" />
<img width="1920" height="1080" alt="Screenshot_20260520_145258" src="https://github.com/user-attachments/assets/4e0b332d-209c-4a90-8364-0ce3ddb67d98" />

