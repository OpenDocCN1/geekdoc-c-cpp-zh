| BGP Neighbor State | Typical Reasons |
|---|---|
| Active | The TCP connection has been completed, but no BGP messages have been sent yet. |
| Opensent | The TCP connection exists, and the router has sent the first message to establish the BGP neighbor relationship (a BGP Open message). |
| Openconfirm | The TCP connection exists and the local router has received an Open message from the other router. The neighbor relationship may still be rejected. |
| Established | The routers are now neighbors/peers and can exchange update messages. |

# Administratively Disabling Neighbors

BGP attaches many configuration parameters to the **neighbor** commands that list a particular neighbor. So, to make it easy to bring down a neighbor, rather than requiring the complete removal of those multiple neighbor commands for that one neighbor, IOS supports the **neighbor shutdown** BGP subcommand. This command administratively disables that BGP neighbor. The **no neighbor shutdown** command then re-enables the neighbor connection. Example 12-3 shows an example, as well as the resulting BGP peer state (Idle).

# **Example 12-3**  *Neighbor State with the Neighbor Shut Down*

```
```text
R1# configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
R1(config)# router bgp 1001
R1(config-router)# neighbor 198.51.100.2 shutdown
*Nov 20 13:05:58.784: %BGP-5-NBR_RESET: Neighbor 198.51.100.2 reset (Admin. shutdown)
R1(config-router)# ^Z
R1#
R1# show ip bgp summary
BGP router identifier 192.0.2.1, local AS number 1001
BGP table version is 1, main routing table version 1

Neighbor        V      AS MsgRcvd MsgSent   TblVer  InQ OutQ Up/Down  State/PfxRcd
198.51.100.2    4       1       0       0        1    0    0 00:00:00 Idle (Admin)
```
```

Take the time to connect the State field value lists at the far right of the output of the **show ip bgp summary** command output at the end of Example 12-3. As mentioned in Table 12-2, the BGP neighbor Idle state simply refers to a neighbor that has been configured with the **neighbor shutdown** command.

# Injecting BGP Table Entries with the network Command

At this point in the sample configurations, R1, the enterprise router, is not advertising any routes to the ISP with BGP. BGP has a couple of methods of injecting information into the BGP table so that BGP will then advertise those routes. The next few pages show how to make that happen with the BGP network command, which is the one method specifically mentioned in the exam topics.