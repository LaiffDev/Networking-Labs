# Project 2: Two Switches, One Bigger LAN

Cisco Packet Tracer lab — part of my hands-on networking practice while working through the [Networking Fundamentals](https://www.youtube.com/playlist?list=PLIFyRwBY_4bRLmKfP1KnZA6rZbRHtxmXi) course and Cisco Networking Academy (CCNA path).

## Objective

Connect two switches together so devices on different switches can still communicate, without needing a separate subnet.

## Topology

```
PC1 ─┐
PC2 ─┤
PC3 ─┼── Switch 1 ── Switch 2 ── PC6
PC4 ─┘                        └── PC7
```

## IP Scheme

| Device | IP Address     | Subnet Mask     | Gateway       |
|--------|----------------|-----------------|---------------|
| PC1    | 192.168.1.10   | 255.255.255.0   | 192.168.1.1   |
| PC2    | 192.168.1.11   | 255.255.255.0   | 192.168.1.1   |
| PC3    | 192.168.1.12   | 255.255.255.0   | 192.168.1.1   |
| PC4    | 192.168.1.13   | 255.255.255.0   | 192.168.1.1   |
| PC6    | 192.168.1.14   | 255.255.255.0   | 192.168.1.1   |
| PC7    | 192.168.1.15   | 255.255.255.0   | 192.168.1.1   |

All hosts remain on the **same subnet** (192.168.1.0/24) despite being spread across two physical switches.

## Steps Taken

- Added a second switch with 2 new PCs (PC6, PC7)
- Assigned PC6 and PC7 IPs on the same subnet as PC1–4 (no new subnet needed)
- Connected Switch 1 to Switch 2 using a straight-through cable (an "uplink")
- Verified connectivity by pinging PC6 from PC1 — successful

## Reflection

**Why didn't PC6/PC7 need a different subnet, even on a separate switch?**
A switch doesn't create a new network — it only extends the existing one. Uplinking Switch 1 to Switch 2 effectively made one larger LAN; both switches are part of the same broadcast domain. A new network is created by a **router**, not a switch.

**What layer does the switch-to-switch uplink operate at?**
Layer 2 (Data Link) — not Layer 1. Every link involves Layer 1 (a physical connection carrying bits), but the layer that matters when asking "what is this link doing" is the layer making the forwarding decision. The uplink still forwards frames based on **MAC addresses**, exactly like any other switch port — no IP/routing logic is involved, so it's Layer 2, same as the PC-to-switch links.

## Key Concepts Demonstrated

- Switches extend a LAN without creating new subnets
- Broadcast domains span multiple switches when uplinked
- Layer 2 forwarding applies uniformly across all switch ports, including uplinks
- Distinction between "a working physical link" (Layer 1) and "how forwarding decisions are made" (Layer 2)

<img width="997" height="660" alt="Screenshot 2026-09-26 134236" src="https://github.com/user-attachments/assets/5390d061-9990-4b09-ad31-1c012eaf4dfe" />
