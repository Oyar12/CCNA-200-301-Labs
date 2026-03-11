# Day 3: TCP/IP and OSI Models 📚

## Objectives
- Master the 4-layer and 5-layer TCP/IP models.
- Understand the 7-layer OSI reference model.
- Analyze the Encapsulation and Decapsulation process.

## Key Concepts
- **Protocols:** A set of rules defining communication between devices (e.g., HTTP, TCP, IP).
- **PDUs (Protocol Data Units):** Data takes different names at each layer (Segments, Packets, Frames, Bits).
- **Interactions:** - *Adjacent-layer:* Communication between layers on the same device.
    - *Same-layer:* Communication between the same layer on different devices (using headers).

## Lab: OSI Model Analysis
I used Cisco Packet Tracer's **Simulation Mode** to inspect network traffic:
1. Generated Layer 7 traffic using `ipconfig /release` and `ipconfig /renew`.
2. Inspected the **Inbound/Outbound PDU details**.
3. Verified the presence of DHCP (L7), UDP (L4), IP (L3), and Ethernet (L2) headers.

<img width="1919" height="1017" alt="Capture d&#39;écran 2026-03-11 130855" src="https://github.com/user-attachments/assets/1d952710-6f0b-4547-8d59-a61f025f5f72" />
<img width="1919" height="1023" alt="Capture d&#39;écran 2026-03-11 130832" src="https://github.com/user-attachments/assets/07b43ca9-0e5f-4fa4-9c52-a356f4d99368" />
