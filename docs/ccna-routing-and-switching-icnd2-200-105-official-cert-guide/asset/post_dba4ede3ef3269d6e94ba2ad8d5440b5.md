
First parameter in the command to each interface IP address on the local router, trying to find a match. However, rather than comparing the entire number in the network command to the entire IPv4 address on the interface, the router can compare a subset of the octets, based on the wildcard mask, as follows:

### Key Topic

- **Wildcard 0.0.0.0:** Compare all 4 octets. In other words, the numbers must exactly match.
- **Wildcard 0.0.0.255:** Compare the first 3 octets only. Ignore the last octet when comparing the numbers.
- **Wildcard 0.0.255.255:** Compare the first 2 octets only. Ignore the last 2 octets when comparing the numbers.
- **Wildcard 0.255.255.255:** Compare the first octet only. Ignore the last 3 octets when comparing the numbers.
- **Wildcard 255.255.255.255:** Compare nothing—this wildcard mask means that all addresses will match the network command.

Basically, a wildcard mask value of 0 in an octet tells IOS to compare to see if the numbers match, and a value of 255 tells IOS to ignore that octet when comparing the numbers.

The network command provides many flexible options because of the wildcard mask. For example, in Router R3, many network commands could be used, with some matching all interfaces, and some matching a subset of interfaces. Table 8-2 shows a sampling of options, with notes.

### Table 8-2 — Example OSPF network Commands on R3, with Expected Results

| Command | Logic in Command | Matched Interfaces |
|---|---|---|
| network 10.1.0.0 0.0.255.255 | Match interface IP addresses that begin with 10.1 | G0/0.341<br>G0/0.342<br>S0/0/0 |
| network 10.0.0.0 0.255.255.255 | Match interface IP addresses that begin with 10 | G0/0.341<br>G0/0.342<br>S0/0/0 |
| network 0.0.0.0 255.255.255.255 | Match all interface IP addresses | G0/0.341<br>G0/0.342<br>S0/0/0 |
| network 10.1.13.0 0.0.0.255 | Match interface IP addresses that begin with 10.1.13 | S0/0/0 |
| network 10.1.3.1 0.0.0.0 | Match one IP address: 10.1.3.1 | G0/0.341 |

The wildcard mask gives the local router its rules for matching its own interfaces. For example, Example 8-2 shows R3 using the network 10.0.0.0 0.255.255.255 area 0 command. However, the wildcard mask allows for many different valid OSPF configurations. For instance, in that same internetwork, Routers R1 and R2 could use the configuration shown in Example 8-3, with two other wildcard masks. In both routers, OSPF is enabled on all the interfaces shown in Figure 8-2.

```text
10.1.1.1      0    FULL/ -    00:00:33   10.1.1.13    Serial0/0/0
10.1.24.4     1    FULL/DR    00:00:35   10.1.3.130   GigabitEthernet0/0.342
10.1.24.4     1    FULL/DR    00:00:36   10.1.3.4     GigabitEthernet0/0.341
```

The detail in the output mentions several important facts, and for most people, working right to left works best in this case. For example, looking at the headings:

- **Interface:** This is the local router's interface connected to the neighbor. For example, the first neighbor in the list is reachable through R3's S0/0/0 interface.
- **Address:** This is the neighbor's IP address on that link. Again, for this first neighbor, the neighbor, which is R1, uses IP address 10.1.13.1.
- **State:** While many possible states exist, for the details discussed in this chapter, FULL is the correct and fully working state in this case.
- **Neighbor ID:** This is the router ID of the neighbor.

Next, Example 8-5 shows the contents of the LSDB on Router R3. Interestingly, when OSPF is working correctly in an internetwork with a single-area design, all the routers will have the same LSDB contents. So, the **show ip ospf database** command in Example 8-5 should list the same exact information, no matter on which of the four routers it is issued.

### Example 8-5 OSPF Database on Router R3 from Figure 8-2

```text
R3# show ip ospf database

            OSPF Router with ID (10.1.13.3) (Process ID 1)

                Router Link States (Area 0)

Link ID         ADV Router      Age        Seq#            Checksum Link count
10.1.1.1        1.1.1.1         498        0x80000006      0x002294 6
2.2.2.2         2.2.2.2         497        0x80000004      0x00EBC6 5
10.1.13.3       10.1.13.3       450        0x80000003      0x001043 4
10.1.24.4       10.1.24.4       451        0x80000003      0x09D7E 4

                Net Link States (Area 0)

Link ID         ADV Router      Age        Seq#            Checksum
10.1.3.4        10.1.24.4       451        0x80000001      0x0045FB
10.1.3.130      10.1.24.4       451        0x80000001      0x00546B
```

For the purposes of this book, do not be concerned about the specifics in the output of this command. However, for perspective, note that the LSDB should list one “Router Link State” (Type 1 Router LSA) for each of the routers in the same area. In this design, all four routers are in the same area, so there are four highlighted Type 1 LSAs listed.

Next, Example 8-6 shows R3's IPv4 routing table with the **show ip route** command. Note that it lists connected routes as well as OSPF routes. Take a moment to look back at Figure 8-2, and look for the subnets that are not locally connected to R3. Then look for those routes in the output in Example 8-6.

The **show ip ospf interface** command lists a single line that mentions that the interface is passive.

Example 8-11 shows these two commands on Router R1, with the configuration shown in the top of Example 8-10. Note that subinterfaces G0/0.11 and G0/0.12 both show up in the output of **show ip ospf interface brief**.

### Example 8-11 Displaying Passive Interfaces

```text
R1# show ip ospf interface brief
Interface   PID   Area            IP Address/Mask    Cost  State Nbrs F/C
Gi0/0/12    1     0               10.1.1.129/25      1     DR    0/0
Gi0/0/11    1     0               10.1.1.1/25        1     DR    0/0
Se0/0/0     1     0               10.1.1.121/25      64    P2P   0/0
Se0/0/1     1     0               10.1.1.121/25      64    P2P   0/0

R1# show ip ospf interface g0/0.11
GigabitEthernet0/0.11 is up, line protocol is up
  Internet Address 10.1.1.1/25, Area 0, Attached via Network Statement
  Process ID 1, Router ID 10.1.1.129, Network Type BROADCAST, Cost: 1
  Topology-MTID    Cost    Disabled    Shutdown      Topology Name
        0           1       no          no            Base
  Transmit Delay is 1 sec, State DR, Priority 1
  Designated Router (ID) 10.1.1.129, Interface address 10.1.1.1
  No backup designated router on this network
  Timer intervals configured, Hello 10, Dead 40, Wait 40, Retransmit 5
    oob-resync timeout 40
    No Hello (Passive interface)
  ! Lines omitted for brevity
```

## Implementing Multiarea OSPFv2

Configuring the routers in a multiarea design is almost just like configuring OSPFv2 for a single area. The only difference is that the configuration places some interfaces on each ABR in different areas. The differences come in the verification and operation of OSPFv2.

This second major section of the chapter provides a second set of configurations to contrast multiarea configuration with single-area configuration. This new scenario shows the configuration for the routers in the multiarea OSPF design based on Figures 8-3 and 8-4. Figure 8-3 shows the internetwork topology and subnet IDs, and Figure 8-4 shows the area design. Note that Figure 8-3 lists the last octet of each router's IPv4 address near each interface, rather than the entire IPv4 address, to reduce clutter.

Take a moment to think about the area design shown in Figure 8-4, and look for the ABRs. Only R1 connects to the backbone area at all. The other three routers are internal routers in a single area. So, as it turns out, three of the four routers have single-area configurations, with all interfaces in the same area.
