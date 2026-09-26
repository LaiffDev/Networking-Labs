# Project 1: Basic LAN + Inter-Network Connectivity

Cisco Packet Tracer lab — part of my hands-on networking practice while working through the [Networking Fundamentals](https://www.youtube.com/playlist?list=PLIFyRwBY_4bRLmKfP1KnZA6rZbRHtxmXi) course and Cisco Networking Academy (CCNA path).

## Objective

Build a LAN with 4 hosts, connect it to a second network via a router, and troubleshoot connectivity issues.

## Topology

```
PC1 ─┐
PC2 ─┤
PC3 ─┼── Switch ── Router ── PC5 (Network B)
PC4 ─┘
```

## IP Scheme

| Device | IP Address     | Subnet Mask     | Gateway       |
|--------|----------------|-----------------|---------------|
| PC1    | 192.168.1.10   | 255.255.255.0   | 192.168.1.1   |
| PC2    | 192.168.1.11   | 255.255.255.0   | 192.168.1.1   |
| PC3    | 192.168.1.12   | 255.255.255.0   | 192.168.1.1   |
| PC4    | 192.168.1.13   | 255.255.255.0   | 192.168.1.1   |
| PC5    | 192.168.2.10   | 255.255.255.0   | 192.168.2.1   |

## Steps Taken

- Created Network A with 4 PCs (PC1–PC4) connected via a switch
- Assigned IPs and confirmed connectivity by pinging PC4 from PC1 (verified in Simulation mode)
- Added a router and Network B with one host (PC5)
- Connected the switch and PC5 to the router
- Configured router interfaces: `192.168.1.1` (facing Network A), `192.168.2.1` (facing Network B)
- Set default gateways on all PCs

## Issue Encountered

Ping from PC4 to PC5 timed out. On inspection, the switch had only 4 Ethernet ports (all in use) and was connected to the router's **Console port** rather than an Ethernet interface — Console is a management-only port and carries no network traffic.

## Fix

Swapped in a switch with more available ports and connected it to the router's Ethernet interface instead. Ping succeeded afterward.

## Key Concepts Demonstrated

- OSI Layer 2 (switch / MAC address forwarding)
- OSI Layer 3 (router / IP addressing and routing)
- Default gateways and why devices on different subnets need a router to communicate
- Physical vs. management ports (Ethernet vs. Console)
- Layer-by-layer troubleshooting: checking the physical connection first before assuming a configuration error

<img width="1080" height="657" alt="Screenshot 2026-09-26 124121" src="https://github.com/user-attachments/assets/7c0b4563-ef09-49ed-8e29-3e7bce754bbe" />
