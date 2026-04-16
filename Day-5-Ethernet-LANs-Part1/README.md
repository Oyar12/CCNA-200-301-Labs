# Jeremy's IT Lab – Day 5: Ethernet LANs (Part 1)

## 1. MAC Address
- **MAC** = Media Access Control
- 6-byte (48-bit) physical address assigned to the device when it is manufactured.
- Also called **BIA** (Burned-in Address).
- Globally unique.

### Structure
- **First 3 bytes** = OUI (Organizational Unique Identifier) – assigned to the manufacturer.
- **Last 3 bytes** = unique to the device itself.
- Written in hexadecimal.

## 2. Ethernet Frame Fields

| Field | Length | Description |
|-------|--------|-------------|
| Preamble | 7 bytes | Alternating 1s and 0s (10101010) – allows devices to synchronize receive clocks |
| SFD (Start Frame Delimiter) | 1 byte | 10101011 – marks the end of preamble and beginning of the rest of the frame |
| Destination MAC | 6 bytes | MAC address of the receiving device |
| Source MAC | 6 bytes | MAC address of the sending device |
| Type / Length | 2 bytes | If ≤ 1536 → length of encapsulated packet (bytes). If ≥ 1536 → type of encapsulated packet (e.g., IPv4 = 0x0800, IPv6 = 0x86DD) |
| Data / Payload | 46–1500 bytes | Encapsulated packet (e.g., IP packet) |
| FCS (Frame Check Sequence) | 4 bytes | CRC algorithm to detect corrupted data |

## 3. Unicast vs Unknown Unicast
- **Unicast frame** : frame destined for a single target device.
- **Unknown unicast frame** : when a switch receives a frame with a destination MAC address not yet in its MAC address table, it floods the frame out all ports (except the receiving port).

## 4. MAC Address Table (Switching)
- Also called **bridging table** or **CAM table**.
- The switch dynamically learns source MAC addresses and maps them to physical switch ports.
- Dynamically learned entries are removed after **5 minutes of inactivity** (default).
- Use command: `show mac address-table`

## 5. CRC (Cyclic Redundancy Check)
- Algorithm run by the FCS field to verify data integrity.
- If CRC fails, the frame is discarded.

## 6. Visual summary (from my notes)
[Insert your handwritten notes screenshots here]

## Next step
Day 6 – Ethernet Switching
