# CCNA 200-301 – Day 14: Subnetting (Part 2)

## 1. Course Summary

This lesson covers advanced IPv4 subnetting concepts, focusing on bitwise operations and formulas to calculate subnets and hosts.

---

### Subnetting Principles

- **Subnetting**: Dividing a large network into smaller, more manageable subnets by borrowing bits from the host portion of an address.
- **Borrowing 1 bit**: Doubles the number of subnets (e.g., from /24 to /25).
- **Formulas**:
    - Number of subnets: `2^x` (x = number of borrowed bits)
    - Number of hosts per subnet: `2^n – 2` (n = number of host bits)

---

## 2. Reference Tables

- Subnetting example (/25):  
  Borrowing one bit splits a /24 into two /25 subnets.
- Subnets/Hosts Table (Class B and Class C examples):  
  | Prefix Length | Number of Subnets | Number of Hosts |
  |---------------|------------------|-----------------|
  | /25           | 512              | 126             |
  | /26           | 1024             | 62              |
  | /27           | 2048             | 30              |
  | ...           | ...              | ...             |

---

## 3. Practice Exercise Notes

_Examples from handwritten notes:_

- **Practice 1:**  
  Divide 192.168.1.0/24 into four /26 subnets:
  - Subnet 1: 192.168.1.0/26
  - Subnet 2: 192.168.1.64/26
  - Subnet 3: 192.168.1.128/26
  - Subnet 4: 192.168.1.192/26

- **Practice 2:**  
  Divide 192.168.255.0/24 into 
  five /27 subnets:
  - Subnet 1: 192.168.255.0/27
  - Subnet 2: 192.168.255.32/27
  - Subnet 3: 192.168.255.64/27
  - Subnet 4: 192.168.255.96/27
  - Subnet 5: 192.168.255.128/27

- For point-to-point links, use /31 subnets.

---

## 4. Key Formulas

- **Number of subnets:** `2^n` (n = number of borrowed bits)
- **Number of hosts per subnet:** `2^h – 2` (h = number of host bits)

---

## 5. Handwritten Notes

_Your handwritten calculations and examples:_

<!-- ![Handwritten Subnetting Notes](image8) -->

---

## 6. Illustrations

<!-- Add your course diagrams here for clarity: -->
<!-- ![Subnetting Bitwise Example](image6) -->
<!-- ![Subnets/Hosts Table](image7) -->

---

## Author

Content and summary by **Oyar12**, based on Jeremy’s IT Lab – CCNA 200-301.
