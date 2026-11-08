| Command | Description |
|---|---|
| show ip ospf interface brief | Lists the interfaces on which the OSPF protocol is enabled (based on the **network** commands), including passive interfaces |
| show ip ospf interface [type number] | Lists detailed OSPF settings for all interfaces, or the listed interface, including Hello and dead timers and OSPF area |
| show ip route ospf | Lists routes in the routing table learned by OSPF |
| show ip ospf neighbor | Lists neighbors and current status with neighbors, per interface |
| show ip ospf | Lists a group of messages about the OSPF process itself, listing the OSPF Router ID in the first line |
| show interfaces | Lists a long set of messages, per interface, that lists configuration, state, and counter information |
| show interfaces description | Lists one line of output per interface with brief status information |

# Table 11-9 Chapter 11 `debug` Command Reference

| Command | Description |
|---|---|
| debug eigrp packets | Lists log messages for EIGRP packets that flow in and out of the router |
| debug ip ospf adj | Issues log messages for adjacency events, meaning events related to routers becoming neighbors |
| debug ip ospf events | Issues log messages for each action taken by OSPF, including the receipt of messages |
| debug ip ospf packet | Issues log messages describing the contents of all OSPF packets |
| debug ip ospf hello | Issues log messages describing Hellos and Hello failures |
| undebug all | EXEC command used to disable all current debug |