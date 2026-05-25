# CCNA 200-301 – Day 15: Subnetting (VLSM)

## 1. VLSM – Quick Theory Recap

- **VLSM (Variable Length Subnet Mask):**  
  A technique to create subnets of different sizes within the same parent network, so that each subnet fits the number of hosts required—no wasted addresses.

- **Why VLSM?**  
  Standard FLSM (Fixed Length Subnet Mask) wastes IP addresses when network segments are of very different sizes. VLSM allows allocating bigger subnets to big LANs and smaller ones to small LANs or WAN links.

- **How VLSM is applied:**
    1. List all network segments and the number of hosts needed for each.
    2. Sort them from largest to smallest.
    3. Assign the largest subnet first (from the start of the address range), then the next largest, and so on.
    4. Continue assigning subnets until all are addressed.

- **Key formulas:**
    - Hosts per subnet: `2^n - 2` (where `n` is the number of host bits)
    - Number of subnets: `2^s` (where `s` is the number of borrowed bits)

---

## 2. Lab – VLSM in Practice

### a) Scenario

- **Network Provided:** `192.168.5.0/24`
- **Requirements:**
  - Tokyo LAN A: 110 hosts
  - Tokyo LAN B: 8 hosts
  - Toronto LAN A: 29 hosts
  - Toronto LAN B: 45 hosts
  - 1 Point-to-point link between routers

### b) Subnet Planning

Assigned VLSM subnets (in order of descending size):

- Tokyo LAN A: `192.168.5.0/25` (126 usable hosts)
- Toronto LAN B: `192.168.5.128/26` (62 usable hosts)
- Toronto LAN A: `192.168.5.192/27` (30 usable hosts)
- Others (example for smaller LANs / point-to-point as needed): `/28`, `/30` or `/31`

### c) Lab Steps Performed

1. **Subnet Calculation & Address Map**
   - Manually planned and written down; cross-checked with Packet Tracer diagrams (see screenshots).

2. **Packet Tracer Implementation**
   - Assigned the first usable IP of each subnet to the PC in the LAN.
   - Assigned the last usable IP address in the subnet to the router.
   - Used `show ip int brief` to verify interface assignments.
   - Configured static routing so all PCs could communicate.

3. **Testing & Troubleshooting**
   - Verified connectivity with `ping` between all PCs.
   - If ping failed, checked subnet masks, interface addresses, and routing settings.

---

## 3. Screenshots & Handwritten Notes

- **Handwritten VLSM calculation plan:**  
  ![Handwritten plan](image12)

- **Network and addressing map:**  
  ![Network map and addressing](image9)

- **Packet Tracer configuration and interface setup:**  
  ![Config interface/PC/route](image10)

- **Ping/routing test results:**  
  ![Ping and routing validation](image11)

---

## Author

Lab and documentation by **Oyar12** – Jeremy’s IT Lab, CCNA 200-301.
