# Subsection 1 @ fffc8068e83c90

| | | | | |
|---|---|---|---||
| ControlArea | fffc8068e83c90 | Starting Sector | 0 Number Of Sectors | 58 |
| Base Pte | fff8da8f4c86d40 | Ptes In Subsect | 58 Unused Ptes | 0 |
| Flags | | d | 0 Protection | 6 |
| Accessed Flink | fffc8068bb7fc0 | Blink | fffc8068bb7fc0 | MappedViews | 2 |

# Subsection 2 @ fffc8068e20e5b0

| | | | | | |
|---|---|---|---||
| ControlArea | fffc8068e83c10 | Starting Sector | 58 Number Of Sectors | 28 |
| Base Pte | fff8da3f4cc5000 | Ptes In Subsect | 28 Unused Ptes | 1d8 |
| Flags | | d Sector Offset | 0 Protection | 6 |
| Accessed Flink | fffc8068e20600 | Blink | fffc8068e20600 | MappedViews | 1 |

Another technique is to display the list of all control areas with the !memusage command. The following example is from the output of this command. (The command might take a long time to complete on a system with a large amount of memory).

```
1kd> |memusage
loading PFN database
loading (100% complete)

Compiling memory usage data (99%).

Zeroed: 98533 ( 394132 kb)
Free: 1405 ( 5620 kb)
Standby: 331221 ( 1324884 kb)
Modified: 83806 ( 335224 kb)
ModifiedNow: 116 ( 464 kb)
Active/Valid: 1556154 ( 624616 kb)
Transition: 5 ( 20 kb)
SLIST/Bad: 1614 ( 6456 kb)
Unknown: 0 ( 0 kb)
TOTAL: 2072854 ( 8291416 kb)

Dangling Yes Commit: 130 ( 520 kb)
Dangling No Commit: 514812 ( 2059248 kb)
Building kernel map
Finished building kernel map

(Master10 for 1c0)

(Master10 for e80)

(Master10 for ec0)

(Master10 for f00)
Scanning PFN database - (02% complete)

(Master10 for de80)
Scanning PFN database - (100% complete)
```