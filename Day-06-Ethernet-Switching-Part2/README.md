# Jeremy's IT Lab – Day 6: Ethernet and Switching (Part 1)

## Theory

### 1. Ethernet frame minimum size
- Minimum frame size = **64 bytes** (header + payload + FCS)
- Minimum payload (packet) = **46 bytes** (padding added if needed)

### 2. ARP (Address Resolution Protocol)
- Maps a known **Layer 3 (IP) address** to a **Layer 2 (MAC) address**
- **ARP Request** = broadcast (sent to all hosts on the network)
- **ARP Reply** = unicast (sent only to the requesting host)
- **ARP table** stores IP → MAC mappings
  - `arp -a` (Windows) or `ip neigh` (Linux)
  - Type: **static** (manual) or **dynamic** (learned via ARP)

### 3. Ping
- Tests reachability
- Measures **round-trip time (RTT)**
- Uses **ICMP Echo Request** and **Echo Reply**

## Lab – Packet Tracer Simulation

### Topology
- Two switches (SW1, SW2) connected via trunk
- Four PCs (PC1, PC2, PC3, PC4) attached to switches
- Initial state: empty MAC address tables on switches, empty ARP tables on PCs

### Tasks performed
1. **Ping from PC1 to PC3** – observed broadcast ARP request, then unicast ARP reply, then ICMP echo/reply.
2. **Used Simulation Mode** to verify each step (see screenshots).
3. Generated traffic to let switches learn MAC addresses dynamically.
4. **Commands used:**
   - `show mac address-table` (view learned MACs)
   - `clear mac address-table dynamic` (remove dynamic entries)
5. Identified MAC addresses of each PC from switch tables.

### Sample output (from my lab)
SW2>show mac address-table
Mac Address Table

Vlan Mac Address Type Ports

1 0001.647b.3119 DYNAMIC Fa0/2
1 0004.9a6e.d870 DYNAMIC Fa0/1
1 0060.5c56.14d3 DYNAMIC Gig0/1
### Key takeaways
- Switches learn MAC addresses dynamically from source MAC of incoming frames.
- Unknown unicast frames are flooded.
- Dynamic MAC entries age out after 5 minutes (default).
<img width="576" height="1280" alt="WhatsApp Image 2026-04-15 at 07 14 0" src="https://github.com/user-attachments/assets/cc8f946c-f650-498e-8607-8c8dd70e5a3c" />
<img width="1911" height="1021" alt="Screenshot 2026-04-03 233717" src="https://github.com/user-attachments/assets/f018b9ae-24a3-4c5c-9b0d-075c7cdaaad9" />
<img width="1919" height="1016" alt="Screenshot 2026-04-03 233504" src="https://github.com/user-attachments/assets/c2d3f8a6-9452-46f4-a0fe-75662c98d9fc" />
