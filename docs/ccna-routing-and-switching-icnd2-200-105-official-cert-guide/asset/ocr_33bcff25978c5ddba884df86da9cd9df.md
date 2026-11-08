Figure 20-6 shows the result when R1, the HSRP active router in Figure 20-5, fails. R1 quits using the virtual IP and MAC address, while R2, the new active router, starts using these addresses. The hosts do not need to change their default router settings at all, with traffic now flowing to R2 instead of R1.

![](bbox=[0.148, 0.183, 0.79, 0.387])

**Host ARP Table**

| IP | MAC |
|---|---|
| 10.1.1.1 | VMAC1 |

**Figure 20-6** _Packets Sent Through R2 (New Active) Once It Takes Over for Failed R1_