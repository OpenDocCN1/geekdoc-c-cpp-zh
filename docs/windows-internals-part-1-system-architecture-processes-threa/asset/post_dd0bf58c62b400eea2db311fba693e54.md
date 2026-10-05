
SessionId: 1 Cid: 2b64 Peb: 0124000 ParentCid: 1d38
DirBase: 2525000 ObjectTable: fffda8f4926c40 HandleCount: 1915.
Image: POWERNT.EXE.

```
1kd>.process /p ffffc8068913e80
Implicit result is now ffffc806*8913e80
1kd>handle
```

0c08: Object: ffffc806f856ea60 GrantedAccess: 00120089 Entry: fda8f491d0020
Object: ffffc806f856ea60 Type: (ffffc806285625c00) File
ObjectHeader: ffffc806f856aa00 (new version)
HandleCount: 1 PointerCount: 30839
Directory Object: 0000000 Name: \WindowsInternals\7Edition\Chapter05\diagrams.pptx (HarddiskVolume2)

Taking the object address (FFFFC806F856A60) and formatting it with dt results in this:

```
1kd dt _nt_file_object ffffc806f856ea60
+0000 Type : 0n
+0002 Size : 0n16
+0008 DeviceObject : 0ffffc06*8408cb40 _DEVICE_OBJECT
+0010 Vpb : 0ffffc06*82feba00_Vpb
+0018 FsContext : 0ffffda8f*5137cd00 Void
+0020 FsContext2 : 0ffffda8f*43c63d590 Void
+0028 SectionObjectPointer : 0ffffc06*8ec0cc58 _SECTION_POINTERS
```

Taking the address of the section object pointers 0ffffc806*8ec0cc58 and formatting it with dt results in this:

```
1kd dt _nt_section_object 0ffffc806*8ec0cc58
+0000 DataSectionObject 0ffffc806*8e83c10 Void
+0008 SharedCacheMap : 0ffffc08*8d967bd0 Void
+0010 ImageSectionObject : (null)
```

Finally, you can use ca to display the control area using the:

```
1kd ca 0ffffc806*8e83c10
ControlArea @ fffffda8f497fdc0 Flink ffffc806ec97f98 Blink
fffffc806ec97f98
```

Section Ref 1 Pfn 58 Mapped Views 2
User Ref 0 WaitForBit 0 Flush Count
File Object ffffc806e85d3d550 ModWriteCount 0 System Views 2
WritableRefs 0

Flags (0080) File Was Purged \WindowsInternals\7Edition\Chapter05\diagrams.pptx

```
Segment @ fffffda8f497fdc0
ControlArea ffffc806e838c100 ExtendInfo 0000000000000000
Total Ptes 80
Segment Size 80000 Committed 0
Flags (<0000> ProtectionMask
```

### Subsection 1 @ fffc8068e83c90

| | | | | |
|---|---|---|---|---|
| ControlArea | fffc8068e83c90 | Starting Sector | 0 Number Of Sectors | 58 |
| Base Pte | fff8da8f4c86d40 | Ptes In Subsect | 58 Unused Ptes | 0 |
| Flags | | d | 0 Protection | 6 |
| Accessed Flink | fffc8068bb7fc0 | Blink | fffc8068bb7fc0 | MappedViews | 2 |

### Subsection 2 @ fffc8068e20e5b0

| | | | | | |
|---|---|---|---|---|---|
| ControlArea | fffc8068e83c10 | Starting Sector | 58 Number Of Sectors | 28 |
| Base Pte | fff8da3f4cc5000 | Ptes In Subsect | 28 Unused Ptes | 1d8 |
| Flags | | d Sector Offset | 0 Protection | 6 |
| Accessed Flink | fffc8068e20600 | Blink | fffc8068e20600 | MappedViews | 1 |

Another technique is to display the list of all control areas with the !memusage command. The following example is from the output of this command. (The command might take a long time to complete on a system with a large amount of memory).

```
1kd> |memusage
loading PFN database
loading (100% complete)
Compiling memory usage (99%).

Zeroed: 98533 (394132 kb)
Free: 1405 (5620 kb)
Standby: 331221 (132488 kb)
Modified: 83806 (335224 kb)
ModifiedNow: 116 (464 kb)
Active/Valid: 1556154 (624616 kb)
Transition: 5 (20 kb)
LIST/Bad: 1614 (6456 kb)
Unknown: 0 (0 kb)
TOTAL: 2072854 (829141 kb)

Dangling Yes Commit: 130 (520 kb)
Dangling No Commit: 514812 (205924 kb)
Building kernel map
(Master10 for 1c0)
(Master10 for e80)
(Master10 for f00)
Scanning PFN database - (2% complete)
(Master10 for de80)
Scanning PFN database - (100% complete)
```

| Usage (In Kb) | Control Valid Dirty PageTables name |
|---|---|---|---|---|
| fffffff 168454 0 0 0 168454 0 |
| fffff0b7e47970d0 64 0 0 0 mapped_file(Microsoft-Windows-Kernel-PnP-Configuration.evxt) |
| fffff0b7e4816560 0 4 0 0 mapped_file(No name for file) |
| fffff0b7e4923c0 40 0 0 0 mapped_file(ED5680AF-0543-4637-A331-850F319) |
| fffff0b7e4a1b430 8 12 0 0 mapped_file(msidll.dll) |
| fffff0b7e4a7c40 128 0 0 0 mapped_file(Microsoft-Windows-Diagnosis-original.evxt) |
| fffff0b7e4a91010 16 8 0 0 16 mapped_file(netjoin.dll)|8a40d0 |
| fffff0b7f8cc360 8212 0 0 0 mapped_file(OUTLOOK.EXE) |
| fffff0b7f8cc1da0 52 28 0 0 mapped_file(verdanab.ttf) |
| fffff0b7f8ce6910 0 4 0 0 mapped_file(No name for file) |
| fffff0b7f8cd35990 0 4 0 0 mapped_file(No name for file) |

The columns point to the control area the mapped file. You can display control areas, segments, and subsections with the kernel debugger! command. For example, to dump the control area for the mapped file Outlook.exe in this example, type the ! command followed by the Control column name, as shown here:

```
1kd> lca fffff0b7f8cc360
ControlArea @ fffff0b7f8cc360
Segment fffff0fd0d8a5570 Flink fffff0c0834f1d0 Blink
Section Ref 1 Pfn Ref 806 Mapped Views 1
User Ref 2 WaitForDel 0 Flush Count c5a0
File Object fffff0b7c0f9e940 ModWriteCount System Views ffff
WritableRefs 80000161
Flags (ao) Image File
```

```
\Program Files (x86)\Microsoft Office\root\Office16\OUTLOOK.EXE
```

| Segment ffffffd0d8a55670 | ControlArea fffff0b7f8cc360 BasedAddress 000000000020000
Total Ptes 1609
Segment Size Committed
Image Commit 1690000 f4 Image Info ffffffd0d8a556b88 0
ProtoPtes ffffffd0d4abbb6000
Flags (c20000) ProtectionMask

+   - Subsection 1 @ fffff0b7f8cc360 Starting Sector 0 Number Of Sectors 2
- ControlArea fffff0b7f8cc360 Ptes In Subsect 1 Unused Ptes 0
- Base Pte 2 Sector Offset 0
- Flags Protection 1

### Subsection 2 @ fffff0b7f8cc4418
ControlArea fffff0b7f8cc360 Starting Sector 2 Number Of Sectors 7b17

| Base Pte | ffffd08ab6b08 | Ptes In Subsect | 63 | Unused Ptes |
|---|---|---|---|---|
| --- | --- | --- | --- | --- |
| Flags | 6 | Sector Offset | 0 | Protection | 3 |

### Subsection 3 @ fffff8c0b7fcc450
ControlArea fffff8c0b7fcc360 Starting Sector 7b19 Number Of Sectors 19a4
Base Pte ffffd08ab722b20 Ptes In Subsect 335 Unused Ptes 0
Flags 2 Sector Offset 0 Protection 1

### Subsection 4 @ fffff8c0b7ffcc488
ControlArea fffff8c0b7ffcc360 Starting Sector 94bd Number Of Sectors 764
Base Pte ffffd08ab744c48 Ptes In Subsect f2 Unused Ptes 0
Flags a Sector Offset 0 Protection 5

### Subsection 5 @ fffff8c0b7ffcc4c0
ControlArea fffff8c0b7ffcc360 Starting Sector 92c1 Number Of Sectors 1
Base Pte ffffd08ab7458a Ptes In Subsect 1 Unused Ptes 0
Flags a Sector Offset 0 Protection 5

### Subsection 6 @ fffff8c0b7ffcc4f8
ControlArea fffff8c0b7ffcc360 Starting Sector 92c2 Number Of Sectors 1
Base Pte ffffd08ab7460a Ptes In Subsect 1 Unused Ptes 0
Flags a Sector Offset 0 Protection 5

### Subsection 7 @ fffff8c0b7ffcc530
ControlArea fffff8c0b7ffcc360 Starting Sector 92c3 Number Of Sectors c62
Base Pte ffffd08ab7468b Ptes In Subsect 18d Unused Ptes 0
Flags 2 Sector Offset 0 Protection 1

### Subsection 8 @ fffff8c0b7ffcc568
ControlArea fffff8c0b7ffcc360 Starting Sector a885 Number Of Sectors 771
Base Pte ffffd08ab75d80d Ptes In Subsect ef Unused Ptes 0
Flags 2 Sector Offset 0 Protection 1

## Working sets

As you've looked at how Windows keeps track of physical memory and how much memory can support, we'll explain how Windows keeps a subset of virtual addresses in physical memory.

As you recall, a subset of virtual pages residing in physical memory is called a working set. There are three kinds of working sets:

- Process working sets These contain the pages referenced by threads within a single process.
- System working sets These contain the resident subset of the pageable system code (for example, ntoskrnl.exe and drivers), pooled pool, and the system cache.
- Working set Each session has a working set that contains the resident subset of the kernel-mode part of the Windows subsystem (Win32k.sys), session pooled, session mapped views, and other session-space drivers.

## Demand paging

Before examining the details of each type of working set, let's look at the overall policy for deciding which pages are brought into physical memory and how long they remain.

The Windows memory manager uses a demand-paging algorithm with clustering to load pages into memory. When a thread receives a page fault, the memory manager loads into the faulted page plus a small number of pages preceding or following it. This strategy attempts to minimize the number of paging IOs a thread will incur. Because programs—especially large ones—tend to execute in small regions of their address space at any given time, loading clusters of virtual pages reduces the number of disk reads. For page faults that reference data pages in images, the cluster size is three pages. For all other page faults, the cluster size is seven pages.

However, a demand-paging policy can result in incurring page faults when threads first executing or when they resume execution at a later point. To optimize the startup of a process (and the system), Windows has an intelligent prefetch engine called the logical prefetcher, described in the next section. Further optimization and prefetching is performed by another component, SuperFetch, described later in the chapter.

## Logical prefetcher and ReadyBoot

During a typical system boot or startup, the order of faults is that some pages are brought in from one part of the file, then from a distant part of the same file, then from a different file, then perhaps from a directory, and again from the first file. This jumping slows down access considerably. Indeed, analysis shows that disk seeks are a dominant factor in slowing boot and application startup. By prefetching batches of pages all at once, we can achieve a sensible ordering of access without excessive backtracking, improving the overall time for system and application startup. The pages that needed can be known in advance because of the high correlation across access boots or application starts.

The prefetcher tries to speed the boot process and application startups by monitoring the data and code accessed by boot and application startups to read in a subsequent boot or application startup to read the code and data. When the prefetcher is active, the memory manager notifies the prefetcher in the kernel of page faults—those that require data read from disk (hard faults) and those that simply require data already in memory to be added to a process's working set (soft faults). The prefetcher monitors the first 10 seconds of application startup. For boot, the prefetcher by default traces from system start until the 30 seconds following the start of the user's shell (typically Explorer), or failing, that through 60 seconds following Windows service initialization or 120 seconds, whichever comes first.
