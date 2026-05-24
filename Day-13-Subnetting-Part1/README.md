# CCNA 200-301 – Day 13: Subnetting (Part 1)

## 1. Course Summary

This session focuses exclusively on the **theory of IP subnetting and address allocation**.

---

### IANA and IP Allocation

- **IANA** (Internet Assigned Numbers Authority) is responsible for distributing IP address blocks to organizations based on size.
- Originally, very large organizations were assigned Class A or B networks; smaller organizations got Class C networks.
- This model resulted in significant waste of address space.

### The Need for Subnetting and CIDR

- To eliminate waste, **CIDR (Classless Inter Domain Routing)** was introduced.
- CIDR allows larger networks to be split into smaller subnets, increasing efficiency and scalability.
- Subnets are now represented in prefix (slash) notation, e.g., `/30`, `/29`, etc.

---

## 2. Key Concepts

- **CIDR Notation Table:**

  | Subnet Mask         | CIDR Notation |
  |---------------------|--------------|
  | 255.255.255.128     | /25          |
  | 255.255.255.192     | /26          |
  | 255.255.255.224     | /27          |
  | 255.255.255.240     | /28          |
  | 255.255.255.248     | /29          |
  | 255.255.255.252     | /30          |
  | 255.255.255.254     | /31          |
  | 255.255.255.255     | /32          |

- **Subnet Example (/30):**
  - Subnet: `203.0.113.0/30`  
  - Usable addresses: `203.0.113.1` and `203.0.113.2` (for point-to-point links)
  - The rest of the parent block (`203.0.113.4` – `203.0.113.255`) can be used for other subnets.

---

## 3. Handwritten Notes

_Summary of the lesson and historical motivation for subnetting:_

<!-- ![Handwritten notes](image8) -->

---

## 4. Illustrations

<img width="576" height="1280" alt="WhatsApp Image 2026-05-24 at  37 38" src="https://github.com/user-attachments/assets/15387e32-e9fd-4048-8d3b-efd9fd741399" />
<img width="1190" height="695" alt="Screenshot 2026-05-21 142543" src="https://github.com/user-attachments/assets/6e360e3f-5630-4912-83b2-521f521240e7" />
<img width="1196" height="707" alt="Screenshot 2026-05-21 142145" src="https://github.com/user-attachments/assets/d71d3839-70a1-4339-9028-c58fa1059bd4" />


---

## Author

Content and summary by **Oyar12**, from Jeremy’s IT Lab – CCNA 200-301.
