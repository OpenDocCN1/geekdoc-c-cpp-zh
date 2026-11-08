![](bbox=[0.089, 0.092, 0.146, 0.128])

# Example 8-15 — *Listing the OSPF-Enabled Interfaces and the Matching OSPF Areas*

```
R1# show ip ospf interface brief
Interface      PID  Area                  IP Address/Mask   Cost  State  Nbrs F/C
Gi0/0.12         1     0                    10.1.2.1/24        1    DR     0/0
Gi0/0.10         1     0                    10.1.1.1/24        1    DR     0/0
Gi0/1            1     4                    10.1.14.1/24       1    BDR    1/1
Se0/0/1          1    23                    10.1.13.1/24      64    P2P    1/1
Se0/0/0          1    23                    10.1.12.1/24      64    P2P    1/1
```

In the output, to correlate the areas, just look at the interface in the first column and the area in the third column. Also, for this example, double-check this information with Figures 8-3 and 8-4 to confirm that the configuration matches the design.

# Verifying Which Router Is DR and BDR

Several show commands identify the DR and BDR in some way, as well. In fact, the show ip ospf interface brief command output, just listed in Example 8-15, lists the local router’s state, showing that R1 is DR on two subinterfaces and R1 is BDR on its G0/1 interface.

Example 8-16 shows two other examples that identify the DR and BDR, but with a twist. The show ip ospf interface command lists detailed output about OSPF settings, per interface. Those details include the RID and interface address of the DR and BDR. At the same time, the show ip ospf neighbor command lists shorthand information about the neighbor’s DR or BDR role as well; this command does not say anything about the local router’s role.

# Example 8-16 — *Discovering the DR and BDR on the R1–R4 Ethernet (from R4)*

```
R4# show ip ospf interface GigabitEthernet 0/0
GigabitEthernet0/0 is up, line protocol is up
  Internet Address 10.1.14.4/24, Area 4, Attached via Network Statement
  Process ID 1, Router ID 10.1.14.4, Network Type BROADCAST, Cost: 1
  Topology-MTID    Cost    Disabled    Shutdown    Topology Name
        0            1        no          no          Base
  Transmit Delay is 1 sec, State DR, Priority 1
  Designated Router (ID) 10.1.14.4, Interface address 10.1.14.4
  Backup Designated Router (ID) 1.1.1.1, Interface address 10.1.1.1
!
! Lines omitted for brevity
R4# show ip ospf neighbor

Neighbor ID      Pri   State      Dead Time       Address        Interface
1.1.1.1           1    FULL/BDR   00:00:33       10.1.14.1      GigabitEthernet0/0
```

First, focus on the highlighted lines from the show ip ospf interface command output. It lists the DR as RID 10.1.14.4, which is R4. It also lists the BDR as 1.1.1.1, which is R1.

The end of the example shows the show ip ospf neighbor command on R4, listing R4’s single neighbor, with Neighbor RID 1.1.1.1 (R1). The command lists R4’s concept of its neighbor state with neighbor 1.1.1.1 (R1), with the current state listed as FULL/BDR. The