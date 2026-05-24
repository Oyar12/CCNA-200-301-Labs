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

<!-- For clarity, add your course slides here if needed: -->
<!-- ![CIDR /30 Example](image6) -->
<!-- ![CIDR Notation Table](image7) -->

---

## Author

Content and summary by **Oyar12**, from Jeremy’s IT Lab – CCNA 200-301.
