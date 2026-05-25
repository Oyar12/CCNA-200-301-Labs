# CCNA 200-301 – Day 15: Subnetting (VLSM)

## 1. VLSM – Quick Theory Recap

- **VLSM (Variable Length Subnet Mask):**  
  A method for creating subnets of different sizes from one large block, maximizing address efficiency.
- **Process:**  
  List all required subnet sizes, assign the largest first, continue with the next largest, and so on until the address space is fully allocated.
- **Key formulas:**  
  - Usable hosts per subnet: `2^n - 2` (n = number of host bits)
  - Number of subnets: `2^s` (s = number of borrowed bits)

---

## 2. Lab – VLSM Subnetting (My Implementation)

**Starting network:** `192.168.5.0/24`  
**Subnet requirements observed in lab:**
- **LAN1:** 64 hosts
- **LAN2:** 45 hosts
- **LAN3:** 14 hosts
- **LAN4:** 9 hosts
- **Point-to-point link (R1-R2):** 2 hosts

**Subnet assignments (from screenshots/capture):**
- **LAN1:** `192.168.5.0/26` (Range: 192.168.5.1–192.168.5.62, Broadcast: .63)
- **LAN2:** `192.168.5.64/26` (Range: 192.168.5.65–192.168.5.126, Broadcast: .127)
- **LAN3:** `192.168.5.128/28` (Range: 192.168.5.129–192.168.5.142, Broadcast: .143)
- **LAN4:** `192.168.5.144/28` (Range: 192.168.5.145–192.168.5.158, Broadcast: .159)
- **Point-to-point:** `192.168.5.224/30` (Range: 192.168.5.225–192.168.5.226, Broadcast: .227)

**Subnetting approach:**  
1. Calculated all subnet sizes with VLSM, starting with the largest.
2. Assigned the first usable address of each subnet to the PC.
3. Assigned the last usable address to the router interface.
4. Configured static routes on both routers to allow full end-to-end connectivity.

---

## 3. Packet Tracer Implementation

- Addressed each LAN with its proper VLSM subnet & assigned interfaces/hosts as per design.
- Used `show ip int brief` to confirm interface IPs and status (see right-side CLI windows in screenshots).
- Performed connectivity tests (see ping window in screenshot).

---

## 4. Verification & Results

- All PCs were assigned the first usable address in their subnet.
- Router interfaces received the last usable address in the subnet.
- After static routing configuration, all hosts could ping each other successfully.

**Troubleshooting**:
- Checked subnet masks, routing tables, and interface status if ping failed at any stage.

---

## 5. Screenshots & Handwritten Notes

- **Packet Tracer addressing & CLI status:**  
  ![Packet Tracer addressing and CLI interface status](image8)
- **Ping and static routing test results:**  
  ![Ping tests and routing verification](image9)

---

## Author

Lab and documentation by **Oyar12** – Jeremy’s IT Lab, CCNA 200-301.
