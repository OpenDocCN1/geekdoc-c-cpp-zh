# High Entropy Virtual Addresses

Dynamic base
NX compatible
Control Flow Guard

Section contains the following load config:

```
00000000 size
       0 time stamp
  0.00 Version
       0 GlobalFlags Clear
       0 GlobalFlags Set
  0 Critical Section Default Timeout
  0 Decommit Free Block Threshold
  0 Decommit Total Prefix Table
0000000000000000 0 Maximum Allocation Size
       0 Virtual Memory Threshold
       0 Process Heap Flags
       0 Affinity Mask
       0 CSD Version
0800 Dependent Load Flag
0000000000000000 0 Edit List
0000000000402066 0 Security Cookie
000000000140151C0 Guard CF address of check-function pointer
000000000140151C8 Guard CF address of dispatch-function pointer
000000000140151D0 Guard CF cf function table
       2A Guard CF function count
00100500 CF Instrumented
       FID table present
       Long jump target table present
      0000 Integrity Flags
      0000 Integrity Catalog
      0000 Code Integrity Catalog Offset
      0000 Code Integrity Reserved
0000000000000000 0 Guard CF address taken IAT table
       0 Guard CF address taken IAT entry count
0000000000000000 0 Guard CF long jump target table
       0 Guard CF long jump target count
0000000000000000 0 Dynamic value relocation table
```

# Guard CF Function Table

Address

```
00000000014001010 _TlgEnableCallback
00000000014001070 SmpSessionComplete
00000000014001080 NtProcessStartupW
00000000014001B30 SmscLoadSubSystemsForMuSession
00000000014001D10 SmscExecuteInitialCommand
00000000014002FB0 SmpExecPgm
```