+   7. ☑ B is correct. Switches operate below the Network layer (think IP) and therefore work at the Data Link layer at the highest. Of course, they also operate at the Physical layer.
+   
+   ☒ A, C, and D are incorrect. Layer 3 switches may operate at the Network layer, but most switches stop at the Data Link layer.

# 640-460: Describe the Purpose of VLANs in a VoIP Environment

+   8. ☑ A is correct. A VLAN implements a unique broadcast domain.
+   
+   ☒ B, C, and D are incorrect. A VLAN does not implement an IPSec subnet, an OSPF server, or a collision domain.

+   9. ☑ A, B, and D are correct. Management is improved through grouping. Security is improved through segregation. Performance is improved through the implementation of broadcast domains that may be smaller than the available switch port count.
+   
+   ☒ C is incorrect. SSL encryption is not impacted by VLANs as it operates at a layer above the Data Link and Network layers where VLANs have impact.

# 640-460: Configure Switched Infrastructure to Support Voice and Data VLANs

+   10. ☑ C is correct. The switchport command is used to assign a port to a VLAN.
+   
+   ☒ A, B, and D are incorrect. The vlan, show vlan, and name commands are used for different functions.

+   11. ☑ A is correct. The vlan command is used to create a VLAN on a Cisco switch.
+   
+   ☒ B, C, and D are incorrect. The show vlan, switchport, and name commands are used for different functions.

+   12. ☑ B is correct. The integrated switch allows the phone to be on one VLAN while the connected PC is on another.
+   
+   ☒ A, C, and D are incorrect. Cisco IP phones do not provide integrated wireless APs, integrated routers, or DHCP servers.