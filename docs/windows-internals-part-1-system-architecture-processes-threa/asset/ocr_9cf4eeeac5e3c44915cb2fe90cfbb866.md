| Usage (In Kb) | | Control Valid Dirty Shared Locked PageTables name |
| fffffff 1684540 0 0 0 0 1684540 0 AWe |
| fffff0b7e47970d0 64 0 0 0 0 mapped_file(Microsoft-Windows-Kernel-PnP%40Configuration.evxt) |
| fffff0b7e4816560 0 4 0 0 0 mapped_file(No name for file) |
| fffff0b7e4923c00 40 0 0 0 0 mapped_file(D-_ED5680AF-0543-4637-A331-850F3190B44J).FSD |
| fffff0b7e4a1b430 8 12 0 0 0 mapped_file(msidll.dll) |
| fffff0b7e4a7c4c0 128 0 0 0 0 mapped_file(Microsoft-Windows-Diagnosis%40original.evxt) |
| fffff0b7e4a91010 16 8 0 0 16 mapped_file(netjoin.dll)|8a404d0 |
| fffff0b7f8cc360 8212 0 0 0 0 mapped_file(OUTLOOK.EXE) |
| fffff0b7f8cc1da0 52 28 0 0 0 mapped_file(verdanab.ttf) |
| fffff0b7f8ce6910 0 4 0 0 0 mapped_file(No name for file) |
| fffff0b7f8cd35990 0 4 0 0 0 mapped_file(No name for file) |

The columns point to the control area the mapped file made. You can display control areas, segments, and subsections with the kernel debugger! command. For example, to dump the control area for the mapped file Outlook.exe in this example, type the ! command followed by the Control column name, as shown here:

```
1kd> lca fffff0b7f8cc360
ControlArea @ fffff0b7f8cc360
Segment fffff0fd0d8a55670 Flink fffff0c08b34f1d0 Blink
Section Ref 1 Pfn Ref 806 Mapped Views 1
User Ref 2 WaitForDel 0 Flush Count c5a0
File Object fffff0b7c0f9e94e0 ModWriteCount System Views ffff
WritableRefs 80000161
Flags (ao) Image File
```

```
\Program Files (x86)\Microsoft Office\root\Office16\OUTLOOK.EXE
```

| Segment ffffffd0d8a55670 |
ControlArea fffff0b7f8cc360 BasedAddress 000000000020000
Total Ptes 1609
Segment Size Committed
Image Commit 1690000 f4 Image Info ffffffd0d8a556b88 0
ProtoPtes ffffffd0d4abbb6000
Flags (c20000) ProtectionMask

+   - Subsection 1 @ fffff0b7f8cc360 Starting Sector 0 Number Of Sectors 2
- ControlArea fffff0b7f8cc360 Ptes In Subsect 1 Unused Ptes 0
- Base Pte 2 Sector Offset 0
- Flags Protection 1

Subsection 2 @ fffff0b7f8cc4418
ControlArea fffff0b7f8cc360 Starting Sector 2 Number Of Sectors 7b17