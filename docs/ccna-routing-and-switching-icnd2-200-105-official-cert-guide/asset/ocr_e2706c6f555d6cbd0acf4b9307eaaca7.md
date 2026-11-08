Table 11-1 summarizes the commands that identify the interfaces on which OSPFv2 and EIGRP are enabled for easier reference.

# Table 11-1   Key Commands to Find Routing Protocol-Enabled Interfaces

| Command | Key Information | Lists Passive Interfaces? |
|---|---|---|
| show ip eigrp interfaces | Lists the interfaces on which EIGRP is enabled (based on the network commands), *excluding* passive interfaces. | No |
| show ip ospf interface brief | Lists the interfaces on which the OSPFv2 is enabled (based on the network router subcommands or ip ospf interface subcommands), *including* passive interfaces. | Yes |
| show ip protocols | Lists the contents of the network configuration commands for each routing process, and lists enabled but passive interfaces. | Yes |

> **NOTE**  All the commands in Table 11-1 list the interfaces regardless of interface status, in effect telling you the results of the network and passive-interface configuration commands.