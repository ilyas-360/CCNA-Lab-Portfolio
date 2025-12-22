# Least Privilege Design
Enterprise Secure Hybrid Infrastructure

---

## Purpose

This document defines how **least privilege access** is enforced across the
enterprise hybrid infrastructure. The design ensures that users, devices,
and services are granted **only the minimum permissions required** to perform
their intended functions, reducing attack surface and limiting blast radius
in the event of compromise.

This approach aligns with **Zero Trust Architecture (ZTA)** principles and
forms the foundation for future **cloud identity integration**.

---

## 1. User Access Privilege

### Objective
Ensure that end-user devices cannot access unauthorized resources or perform
lateral attacks against other endpoints.

### Access Granted
- Access only to required VLANs
- Default gateway access via HSRP virtual IP
- DNS and DHCP services
- Internet access through controlled NAT

### Access Denied
- Direct access to management VLANs
- Direct access to infrastructure devices
- Inter-user lateral movement within the same VLAN

### Design Controls
- Network segmentation enforced at the distribution layer
- Access-layer architecture designed to support:
  - Private VLANs (PVLANs), or
  - Port Isolation mechanisms

These controls ensure that even if two endpoints reside in the same VLAN,
they are logically prevented from directly communicating with or attacking
each other without explicit policy authorization.

This design aligns with Zero Trust principles by treating all endpoints as
untrusted by default, regardless of VLAN membership.

---

## 2. Network Device Privilege

### Objective
Protect network infrastructure from unauthorized access and configuration
changes.

### Controls Implemented
- Role-based local user accounts
- Encrypted credentials using enable secrets
- Secure remote management via SSH only
- VTY access restricted using access-class ACLs
- Centralized logging to a dedicated logging host
- NTP synchronization for audit consistency

### Access Denied
- Telnet and insecure management protocols
- Management access from user VLANs
- Unauthorized configuration changes

---

## 3. Management Plane Privilege

### Objective
Isolate and protect the management plane from the data and control planes.

### Controls Implemented
- Dedicated management VLAN (VLAN 99)
- Management IP addressing separated from user traffic
- SNMP configured as read-only
- Logging and monitoring directed to centralized services

### Access Denied
- User-initiated access to management interfaces
- East-west traffic between management interfaces

---

## 4. Routing and Control Plane Privilege

### Objective
Ensure that routing and control protocols operate only between trusted devices.

### Controls Implemented
- OSPF limited to infrastructure interfaces
- Passive interfaces used to prevent unnecessary adjacency formation
- Loopback interfaces used for stable router identification
- Default route propagation controlled at the edge

### Access Denied
- OSPF participation from access-layer endpoints
- Unauthorized route injection

---

## 5. External Access and NAT Privilege

### Objective
Control how internal systems access external networks.

### Controls Implemented
- NAT/PAT enforced at the edge router
- Static NAT used only for explicitly published services
- ACLs restrict which internal networks are allowed outbound translation

### Access Denied
- Direct public IP exposure of internal systems
- Unauthorized inbound connections

---

## 6. Identity and Zero Trust Alignment

Although this environment is network-centric, the design is intentionally
aligned with **identity-based security models**, enabling future integration
with:

- Cloud Identity Providers (Azure AD / AWS IAM)
- Device posture validation
- Conditional access policies
- Identity-aware proxies

The network enforces **policy boundaries**, while identity will later enforce
**who** and **what** is allowed to cross them.

---

## 7. Security Outcomes

This least privilege design achieves the following:

- Reduced lateral movement risk
- Minimized attack surface
- Clear separation of duties
- Strong foundation for cloud identity adoption
- Enterprise-ready Zero Trust posture

---

## Status

- Design: Implemented
- Validation: Ongoing
- Cloud Identity Integration: Planned
