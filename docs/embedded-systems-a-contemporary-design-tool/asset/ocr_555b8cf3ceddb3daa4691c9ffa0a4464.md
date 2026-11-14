# 4.12.2 Refresh Address

The refresh address is not the same address as is used by the normal read or write operations. To provide the address, a 12-bit binary counter is used. The counter should be incremented following the completion of each row refresh operation. The address counter appears in Figure 4.24.

![](bbox=[0.352, 0.203, 0.656, 0.302])

Figure 4.24 Refresh Address Generator

During a normal read or write operation, the row addresses to the DRAM are provided by the source executing the operation. During a refresh, they are given by the refresh address counter. Thus, the DRAM address lines must provide row, then column addresses during normal operation and refresh row addresses during the refresh cycle. Selection among the three alternatives is shown in Figure 4.25.

![](bbox=[0.254, 0.472, 0.742, 0.872])

Figure 4.25 Address Source Control