
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
