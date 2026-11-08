Conversely, Figure 17-7 shows the reverse flow, with a packet sent by the server back toward PC1. In this case, the packet’s TCP header has a source port of 21, so the ACL must check the source port value of 21, and the ACL must be located on different interfaces. In this case, the eq 21 parameters follow the source address field, but come before the destination address field.

![](bbox=[0.1341, 0.1972, 0.8008, 0.3943])

# **Figure 17-7** *Filtering Packets Based on Source Port*