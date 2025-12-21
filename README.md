Enterprise Secure Hybrid Infrastructure (CCNA Mega Lab)
🎯 Strategic Objective

This repository documents a high-availability, multi-site enterprise network designed as a foundational underlay for Hybrid Cloud and Identity-centric architectures.

The lab mirrors real-world enterprise design patterns used to securely connect on-premises infrastructure to Cloud Identity Providers such as Microsoft Entra ID (Azure AD) or AWS IAM, emphasizing segmentation, redundancy, and controlled administrative access.

🛡️ Security & Identity-Oriented Design

Although this project is based on CCNA objectives, the implementation prioritizes Identity-First and Zero Trust principles commonly used in modern enterprise and cloud environments.

Zero Trust Foundations

Port Security and DHCP Snooping enforce trusted endpoint identity (MAC/IP bindings).

Unauthorized devices are prevented from participating in the network.

Micro-Segmentation

VLAN-based segmentation strictly isolates user, server, wireless, and management traffic.

This design directly maps to Cloud Network Security Groups (NSGs) and segmentation policies.

Administrative Access Protection

Implemented the Principle of Least Privilege (PoLP) via local AAA and role-based privilege levels.

SSH-only management access.

Management-plane ACLs restrict administrative reachability to authorized hosts only.

🛠️ Technical Scope

Redundancy & High Availability

HSRP for First-Hop Redundancy

EtherChannel (PAgP & LACP) for link and path resilience

Scalability & Control

VTPv2 for controlled VLAN propagation

Hierarchical Core / Distribution / Access design

Routing & Edge Connectivity

Multi-area OSPF

NAT / PAT for secure external access

📁 Repository Structure
├── configs/          # Hardened device configurations (credentials redacted)
├── topology/         # Logical and physical network diagrams
├── security-audit/   # ACL logic and access-control decisions
└── verification/     # HSRP failover and security enforcement logs

🚀 The Path to Cloud Identity

This project validates my mastery of enterprise networking fundamentals as the secure underlay for cloud and identity services.

The next phase of this roadmap includes:

Site-to-Site VPN integration with Azure / AWS

Hybrid identity authentication using SAML / OIDC

Identity-aware access enforcement aligned with Zero Trust architectures

Ilyas Benkhadra
Cybersecurity & Cloud Identity Engineering
