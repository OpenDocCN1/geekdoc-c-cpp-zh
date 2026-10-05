| Base Pte | ffffd08ab6b008 | Ptes In Subsect | f63 | Unused Ptes | 0 |
| --- | --- | --- | --- | --- | --- |
| Flags | 6 | Sector Offset | 0 | Protection | 3 |

Subsection 3 @ ffff8c0b7fcc450
ControlArea ffff8c0b7f7cc360 Starting Sector 7b19 Number Of Sectors 19a4
Base Pte ffffd08ab722b20 Ptes In Subsect 335 Unused Ptes 0
Flags 2 Sector Offset 0 Protection 1

Subsection 4 @ ffff8c0b7fcc488
ControlArea ffff8c0b7f7cc360 Starting Sector 94bd Number Of Sectors 764
Base Pte ffffd08ab744c48 Ptes In Subsect f2 Unused Ptes 0
Flags a Sector Offset 0 Protection 5

Subsection 5 @ ffff8c0b7fcc4c0
ControlArea ffff8c0b7f7cc360 Starting Sector 92c1 Number Of Sectors 1
Base Pte ffffd08ab74c58a Ptes In Subsect 1 Unused Ptes 0
Flags a Sector Offset 0 Protection 5

Subsection 6 @ ffff8c0b7fcc4f8
ControlArea ffff8c0b7f7cc360 Starting Sector 92c2 Number Of Sectors 1
Base Pte ffffd08ab74c60a Ptes In Subsect 1 Unused Ptes 0
Flags a Sector Offset 0 Protection 5

Subsection 7 @ ffff8c0b7fcc530
ControlArea ffff8c0b7f7cc360 Starting Sector 92c3 Number Of Sectors c62
Base Pte ffffd08ab74c68b Ptes In Subsect 18d Unused Ptes 0
Flags 2 Sector Offset 0 Protection 1

Subsection 8 @ ffff8c0b7fcc568
ControlArea ffff8c0b7f7cc360 Starting Sector a885 Number Of Sectors 771
Base Pte ffffd08ab75d80d Ptes In Subsect ef Unused Ptes 0
Flags 2 Sector Offset 0 Protection 1

# Working sets

As you've looked at how Windows keeps track of physical memory and how much memory it can support, we'll explain how Windows keeps a subset of virtual addresses in physical memory.

As you recall, a subset of virtual pages residing in physical memory is called a working set. There are three kinds of working sets:

+   - Process working sets These contain the pages referenced by threads within a single process.
- System working sets These contain the resident subset of the pageable system code (for\ example, ntoskrnl.exe and drivers), pooled pool, and the system cache.
- Working's working set Each session has a working set that contains the resident subset of the
kernel-mode session-specific data structures allocated by the kernel-mode part of the Windows
subsystem (Win32k.sys), session pooled, session mapped views, and other session-space
drivers.

412 CHAPTER 5 Memory management