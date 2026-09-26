# Project 3: Three-Department Office Network

Cisco Packet Tracer lab — part of my hands-on networking practice while working through the [Networking Fundamentals](https://www.youtube.com/playlist?list=PLIFyRwBY_4bRLmKfP1KnZA6rZbRHtxmXi) course and Cisco Networking Academy (CCNA path).

## Objective

Build a small office network with 3 separate departments, each on its own subnet, all routing through a single router. The IT department deliberately spans two switches, reusing the pattern from Project 2.

## Topology

```
Sales (192.168.10.0/24) ─────┐
  3 PCs, 1 switch              │
                                │
IT (192.168.20.0/24) ─────────┼── Router
  2 PCs, 2 switches (uplinked)  │
                                │
Management (192.168.30.0/24) ─┘
  2 PCs, 1 switch
```

## IP Scheme

| Department  | Network           | Gateway        |
|-------------|-------------------|----------------|
| Sales       | 192.168.10.0/24   | 192.168.10.1   |
| IT          | 192.168.20.0/24   | 192.168.20.1   |
| Management  | 192.168.30.0/24   | 192.168.30.1   |

## Steps Taken

- Built each department with its own switch(es) and PCs, assigning IPs and gateways per department
- IT department spans two switches (same uplink pattern as Project 2), but keeps its own subnet since it connects to the router independently
- Connected each department's switch to its own router interface, with a matching gateway IP
- Confirmed full connectivity: every PC could ping every PC in every other department

## Self-Inflicted Troubleshooting Exercise

After confirming full connectivity, I deliberately introduced a fault of my own choosing (without pre-planning the fix) to practice independent diagnosis.

### Symptom
Pings between departments stopped working entirely. All links from the department switches to the router showed a **red** connection indicator.

### Diagnostic Process
1. Started at **Layer 1** (physical layer) rather than assuming a configuration issue — noticed the Sales-to-router cable was red.
2. Checked every other switch-to-router link and found the **same red status on all of them**. Recognized that a shared symptom across multiple, otherwise-unrelated connections points to one common cause rather than several independent faults.
3. Since the router was the one element common to every failing link, inspected it directly — found the correct IP addresses configured on each interface, but the interface **status was "Down."**

### Fix
Changed each affected router interface from "Down" to "Up." Connectivity between all departments was restored immediately.

## Key Concepts Demonstrated

- Router interfaces are **administratively shut down by default** and must be manually enabled — a genuine real-world "first setup" gotcha, not just a Packet Tracer quirk
- Recognizing a **shared symptom across multiple connections** points to a common root cause, rather than treating each as a separate problem
- Consistent layer-by-layer troubleshooting: physical layer checked first, before questioning configuration
- Scaling a previously learned pattern (multi-switch LAN from Project 2) into a larger, multi-department design

<img width="1617" height="659" alt="project_3" src="https://github.com/user-attachments/assets/b28896cd-95d2-41ca-ac67-c22a587591a4" />
