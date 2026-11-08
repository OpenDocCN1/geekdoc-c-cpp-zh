![](bbox=[0.136, 0.116, 0.543, 0.316])

| Role | Router | Address |
|---|---|---|
| AVG | R1 | 10.1.1.1 |
| Forwarder | R1 | VMAC1 |
| Forwarder | R2 | VMAC2 |

# **Figure K-3**  *GLBP Directs Host A by Sending Back ARP Reply with R1’s VMAC1*

The figure shows three messages, top to bottom, with the following action:

+   1. Host A has no ARP table entry for its default router, 10.1.1.1, so host A sends an ARP Request to learn 10.1.1.1’s MAC address.
+   2. The GLBP AVG, R1 in this case, sends back an ARP Reply. The AVG chooses to include its own virtual MAC address in the ARP Reply, VMAC1.
+   3. Future IP packets sent by host A are encapsulated in Ethernet frames, destined to VMAC1, so that they arrive at R1.

From now on, host A sends off-subnet packets to R1 due to host A’s ARP table entry for its default gateway (10.1.1.1). Host A’s ARP table entry for 10.1.1.1 now refers to a MAC address on R1 (VMAC1), so packets host A sends off-subnet flow through R1.

To balance the load, the AVG answers each new ARP Request with the MAC addresses of alternating routers. Figure K-4 continues the load-balancing effect with the ARP Request for 10.1.1.1 coming from host B. The router acting as AVG (R1) still sends the ARP Reply, but this time with R2’s virtual MAC (VMAC2).

![](bbox=[0.136, 0.651, 0.543, 0.849])

| Role | Router | Address |
|---|---|---|
| AVG | R1 | 10.1.1.1 |
| Forwarder | R1 | VMAC1 |
| Forwarder | R2 | VMAC2 |

# **Figure K-4**  *GLBP Directs Host B by Sending Back ARP Reply with R2’s VMAC2*