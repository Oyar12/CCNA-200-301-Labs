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

<img width="1919" height="1021" alt="Screenshot 2026-05-23 120906" src="https://github.com/user-attachments/assets/d6fbf57d-0b72-489f-8c09-2058f3f2ca84" /><img width="576" height="1280" alt="WhatsApp Image 2026-05-24 at 44" src="https://github.com/user-attachments/assets/ab228660-f572-4a6c-bf38-09f7a7651947" />
<img width="1919" height="1020" alt="Screenshot 2026-05-23 122419" src="https://github.com/user-attachments/assets/a52ae285-67af-446c-b0cc-63760a0c590f" />

---

## Author

Lab and documentation by **Oyar12** – Jeremy’s IT Lab, CCNA 200-301.
