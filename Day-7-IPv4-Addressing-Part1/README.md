# Jeremy's IT Lab – Day 7: IPv4 Addressing (Part 1)

## 1. Network Layer (Layer 3)
- Provides connectivity between end hosts on **different networks** (outside the LAN).
- Provides **logical addressing** (IP addresses).
- Routes packets between subnets.
- Routers / gateways operate at Layer 3.

## 2. IPv4 Address
- Size: **32 bits** (4 bytes).
- Written in **dotted decimal** (e.g., `192.168.1.254`).
- Each group of 8 bits = **octet**.

### Structure
- **First 24 bits** = network portion (in many examples, but depends on subnet mask).
- **Remaining 8 bits** = host portion (in a /24 network).

## 3. Address Classes (Classful addressing)

| Class | First octet range | Prefix length (default) | Note |
|-------|------------------|------------------------|------|
| A | 0 – 127 | /8 | First bit always 0 |
| B | 128 – 191 | /16 | First two bits 10 |
| C | 192 – 223 | /24 | First three bits 110 |
| D | 224 – 239 | N/A (multicast) | |
| E | 240 – 255 | N/A (reserved) | |

## 4. Loopback Address
- Range: `127.0.0.0` – `127.255.255.255`
- Used to test the **network stack** on the local device (OSI / TCP/IP).

## 5. Prefix Length (Subnet Mask)
- Indicates the network portion of the IP address.
- Examples:
  - Class A: /8 (e.g., `10.0.0.0/8`)
  - Class B: /16 (e.g., `172.16.0.0/16`)
  - Class C: /24 (e.g., `192.168.1.0/24`)

## 6. Network Address
- Host portion = all **0s**.
- Example: `192.168.1.0/24`
- **Cannot be assigned to a host.**

## 7. Broadcast Address
- Host portion = all **1s**.
- Example: `192.168.1.255/24`
- Used to send a packet to **all hosts** on the local network.
- **Cannot be assigned to a host.**

## Example summary (from my notes)

| Class | Example IP | Default mask | Network address | Broadcast |
|-------|------------|--------------|-----------------|-----------|
| A | 10.0.0.1 | /8 | 10.0.0.0 | 10.255.255.255 |
| B | 172.16.5.1 | /16 | 172.16.0.0 | 172.16.255.255 |
| C | 192.168.1.254 | /24 | 192.168.1.0 | 192.168.1.255 |

## Next step
Day 8 – IPv4 Addressing (Part 2) – subnetting
<img width="576" height="1280" alt="WhatsApp Image 2026-04-15 at 0714 00" src="https://github.com/user-attachments/assets/61c91349-2b8d-43b0-b222-04c0103a5fb2" />
<img width="576" height="1280" alt="WhatsApp Image 2026-04-15 at 014 01" src="https://github.com/user-attachments/assets/33a64223-4e8f-490a-9a8d-4170edd523ac" />
