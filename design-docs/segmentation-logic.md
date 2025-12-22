# Segmentation Logic & Security Boundaries

## Objective
This document explains how traffic segmentation is intentionally designed
to enforce security, availability, and identity-based access control.

Segmentation is implemented using:
- VLAN separation
- Layer 3 gateways at the distribution layer
- Access-layer enforcement controls
- Policy-ready boundaries for future Zero Trust integration

---

## Layered Segmentation Model

### Core Layer
- Pure transport and routing
- No user-facing VLANs
- OSPF backbone with route summarization
- Acts as a trusted but tightly controlled transit layer

### Distribution Layer
- Primary enforcement boundary
- Default gateway (HSRP) for all VLANs
- Inter-VLAN routing controlled centrally
- DHCP relay and identity handoff point

### Access Layer
- No routing
- Port-level security enforcement
- Identity signals originate here (user, device, voice)

---

## VLAN-Based Segmentation

| VLAN | Role | Trust Level |
|----|----|----|
| VLAN 10 | User Data | Low |
| VLAN 20 | Voice | Medium |
| VLAN 30 | Servers | High |
| VLAN 40 | Wireless | Low |
| VLAN 99 | Management | Restricted |

Each VLAN represents a **security zone**, not just a broadcast domain.

---

## Access Layer Enforcement

Implemented controls:
- Port Security (sticky MAC)
- DHCP Snooping
- Dynamic ARP Inspection
- BPDU Guard + PortFast
- Explicit trunk restrictions

These controls prevent:
- Rogue DHCP servers
- ARP spoofing
- Unauthorized switch insertion
- MAC flooding attacks

---

## Identity Awareness (Foundational)

Although identity providers are not yet integrated, the network is prepared for:
- User-based access policies
- Device posture validation
- NAC / Zero Trust enforcement
- Cloud Identity federation

The access layer becomes the **identity signal source**,
while the distribution layer becomes the **policy enforcement point**.

---

## Business Alignment

This segmentation design supports:
- High availability (HSRP, dual distribution)
- Operational stability
- Predictable failure domains
- Future cloud identity and Zero Trust expansion
