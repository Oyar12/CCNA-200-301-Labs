# Day 10 - Understanding the IPv4 Header

This repository contains notes for **Day 10**, focusing on an in-depth study of the IPv4 header structure. Mastering packet formats is a foundational networking skill, critical for traffic analysis, network troubleshooting, and cybersecurity monitoring (such as SOC analysis and Blue Team operations).

## IPv4 Header Fields Detailed

### 1. Version (4 bits)
* Identifies the version of IP used.
* **IPv4** = 4 (Binary: `0100`)
* **IPv6** = 6 (Binary: `0110`)

### 2. Internet Header Length - IHL (4 bits)
* The final field of the IPv4 header (Options) is variable in length, so this field is necessary to indicate the total length of the header.
* Identifies the length of the header **in 4-byte increments**.
* **Minimum value**: 5 (5 x 4-bytes = **20 bytes**).
* **Maximum value**: 15 (15 x 4-bytes = **60 bytes**).
* Binary calculation for max value: `1 1 1 1` -> $8 + 4 + 2 + 1 = 15$.

### 3. DSCP - Differentiated Services Code Point (6 bits)
* Used for **QoS (Quality of Service)**.
* Used to prioritize delay-sensitive data such as streaming voice, video, etc.

### 4. Identification (16 bits)
* If a packet is fragmented due to being too large, this field is used to identify which packet the fragment belongs to.
* All fragments of the same packet will have their own IPv4 header with the same value in this field.
* Packets are fragmented if they are larger than the **MTU (Maximum Transmission Unit)**.

### 5. Flags (3 bits)
* Used to control and identify fragments.
* **Bit 0**: Reserved, always set to `0`.
* **Bit 1**: Don't Fragment (**DF bit**), used to indicate a packet that should not be fragmented.
* **Bit 2**: More Fragments (**MF bit**), set to `1` if there are more fragments in the packet, and set to `0` for the last fragment.
* *Note*: Unfragmented packets will always have their MF bit set to `0`.

### 6. Fragment Offset (13 bits)
* Used to indicate the position of the fragment within the original, unfragmented IP packet.
* Allows fragmented packets to be reassembled properly even if the fragments arrive out of order.

### 7. Time To Live - TTL (8 bits)
* A router will drop a packet with a TTL of `0`.
* Used to **prevent infinite routing loops**.
* Originally designed to indicate the packet's maximum lifetime in seconds.
* In practice, it indicates a **'hop count'**: each time the packet arrives at a router, the router decreases the TTL value by 1.

### 8. Protocol (8 bits)
* Indicates the protocol of the encapsulated L4PDU (Layer 4 Protocol Data Unit).
* Common protocol values:
  * **6**: TCP
  * **17**: UDP
  * **1**: ICMP
  * **89**: OSPF (Dynamic Routing Protocol)
* *Reference*: [List of IP protocol numbers (Wikipedia)](https://en.wikipedia.org/wiki/List_of_IP_protocol_numbers)

---
*Notes compiled from Jeremy's IT Lab course.*
