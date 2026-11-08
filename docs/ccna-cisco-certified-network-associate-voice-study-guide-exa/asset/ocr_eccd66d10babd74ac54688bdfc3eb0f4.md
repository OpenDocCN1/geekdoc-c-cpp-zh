port; however, the 7910G+SW model does, with the +SW signifying a switch is integrated into the model. Additionally, the 7905G model does not support the PC switch port, but the 7912G model does. As you can see, there is a lot of variety in the Cisco phones. Cisco sells and supports both wired and wireless IP phones, which are covered in more detail in Chapter 10.

# ## CERTIFICATION OBJECTIVE 2.02

# # 640-460: Describe the Purpose of VLANs in a VoIP Environment

Cisco switches, as well as most enterprise switches, support VLANs. VLANs are useful in a VoIP environment, and you'll need to understand why for the CCNA Voice and CCVOICE exams. You should understand what a VLAN is, how the VLAN trunking protocol works, and the use of VLANs in VoIP networks.

# ## VLANs and VoIP

VLANs provide multiple broadcast domains within a single switch or within a switch environment with multiple connected switches. Normally, without VLANs, if a broadcast is sent into a switch port, it is forwarded out on all other switch ports. VLANs allow you to break these ports apart into logical switches. The beauty of this feature is that the VLANs can even span multiple switches using VLAN trunking protocols.

As an example, imagine you have a small 12-port switch. You want six of the ports to be configured with IP addresses from 10.10.10.14 through 10.10.10.19. You want the other six ports to be configured with IP addresses from 10.10.11.14 through 10.10.11.19. While you could statically configure the IP addresses without the requirement of a VLAN, this would not result in separate broadcast domains. The best way to implement this configuration is as follows:

+   - Create one VLAN for the 10.10.10.x network and another for the 10.10.11.x network.
+   - Assign the appropriate switch ports to each VLAN.
+   - Configure the IP addresses appropriately using DHCP or static configurations.