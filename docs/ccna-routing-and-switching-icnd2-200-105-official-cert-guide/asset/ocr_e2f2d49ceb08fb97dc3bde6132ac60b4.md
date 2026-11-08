![](bbox=[0.145, 0.078, 0.805, 0.33])

*Figure 27-4  Basic Networking in a Virtualized Host with a Virtual Switch*

Interestingly, the vSwitch can be supplied by the hypervisor vendor or by Cisco. For instance, Cisco's data center switch product line, Cisco Nexus switches, includes the Nexus 1000v (v for virtual). At your option, you can use the vSwitch included by the hypervisor, or install the Cisco Nexus 1000v (or similar products). The Nexus 1000v then supports some features unique to the Cisco Nexus series of switches. (Note that the Cisco data center switches, and the NX-OS operating system that runs on the Nexus models of switches, are covered in the CCNA, CCNP, and CCIE Data Center certifications.)

The networking details shown in Figure 27-4 show just the basics, but two important points remain for this chapter's buildup to cloud. First, networking in the data center has many options. Each VM can be in its own VLAN, or share the same VLAN, or even use VLAN trunking to the VM itself. Second, that configuration can be easily done from within the same virtualization software that controls the VMs. That programmability allows the virtualization software to move VMs between hosts (servers), and reprogram the vSwitches so that the VM has the same networking capabilities no matter where the VM is running.

# ### The Physical Data Center Network

To pull these ideas together, next consider what happens with the physical network in a virtualized data center. Each host—that is, the physical host—needs a physical connection to the network. Looking again at Figure 27-4, that host, with two physical NICs, needs to connect those two physical NICs to a LAN in the data center.

Figure 27-5 shows the traditional cabling for a data center LAN. Each taller rectangle represents one rack inside a data center, with the tiny squares representing NIC ports, and the lines representing cables.

Often, each host is cabled to two different switches in the top of the rack—called Top of Rack (ToR) switches—to provide redundant paths into the LAN. Each ToR switch acts as an access layer switch from a design perspective. Each ToR switch is then cabled to an End of Row (EoR) switch, which acts as a distribution switch, and also connects to the rest of the network.