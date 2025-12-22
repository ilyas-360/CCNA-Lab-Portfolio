# Zero Trust Foundations – Network Underlay Perspective

## Purpose
This document explains how Zero Trust security principles are enforced at the **network underlay level** within this lab. While no cloud Identity Provider (IdP) is integrated yet, the architecture intentionally mirrors the controls required to support future **identity-centric security models** (e.g., Microsoft Entra ID, AWS IAM).

This file focuses on **design intent**, not cloud deployment claims.

---

## Zero Trust Principle: “Never Trust, Always Verify”

In Zero Trust architectures, trust is not based on network location.  
Instead, **every device, user, and session must be verified**.

At the network layer, this verification begins **before identity reaches the cloud**.

This lab enforces Zero Trust concepts through the following mechanisms:

---

## 1. Explicit Network Segmentation (Micro-Segmentation)

### Implementation
- VLAN-based segmentation per function:
  - VLAN 10 – PCs
  - VLAN 20 – Phones
  - VLAN 30 – Servers
  - VLAN 40 – Wi-Fi
  - VLAN 99 – Management
- Separate VLANs per site (Office A / Office B)
- Trunk links explicitly restrict allowed VLANs
- Native VLAN moved to unused VLAN 1000

### Zero Trust Mapping
| Network Control | Identity Meaning |
|-----------------|------------------|
| VLAN isolation | Identity boundary |
| Trunk allow-lists | Explicit trust definition |
| Dedicated Mgmt VLAN | Admin identity separation |

This mirrors how **cloud security groups and identity scopes** operate.

---

## 2. Identity-Aware Device Admission

### Implementation
- DHCP Snooping enabled on all user VLANs
- Dynamic ARP Inspection (DAI) enforced
- Port Security with sticky MAC addresses
- Access ports explicitly configured (no DTP)

### Zero Trust Mapping
| Network Control | Identity Meaning |
|-----------------|------------------|
| DHCP Snooping | IP–MAC binding |
| DAI | Anti-spoofing |
| Port Security | Device identity enforcement |

Before any user identity can authenticate to an IdP,  
the **device itself must be trusted**.

---

## 3. Least-Privilege Network Access

### Implementation
- ACLs applied to management plane
- SSH-only administrative access
- Management reachability restricted to specific subnets
- Unused ports administratively shut down

### Zero Trust Mapping
| Network Control | Identity Meaning |
|-----------------|------------------|
| Management ACLs | Admin scope limitation |
| SSH-only access | Secure authentication channel |
| Disabled ports | Attack surface reduction |

This aligns directly with **Conditional Access** concepts used in cloud identity platforms.

---

## 4. High Availability as a Security Requirement

Zero Trust assumes failure and compromise.

### Implementation
- HSRP for gateway redundancy
- EtherChannel for link resilience
- Dual core and distribution switches
- OSPF dynamic routing

Availability ensures that **identity enforcement remains consistent**, even during failures.

---

## What This Lab Does NOT Claim

- No cloud IdP integration is implemented yet
- No SAML, OIDC, or OAuth flows are configured
- No endpoint posture validation exists at this stage

These are **future phases**, documented in the project roadmap.

---

## Strategic Intent

This lab establishes a **Zero Trust–ready network underlay**.

Future work will extend this foundation to:
- Site-to-Site VPNs
- Cloud identity enforcement
- Identity-aware access policies

The network is designed to **support identity**, not bypass it.

---

## Summary

Zero Trust does not begin in the cloud.  
It begins with **intentional network design**.

This repository documents that foundation.
