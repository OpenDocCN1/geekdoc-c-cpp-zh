Lines 0–3 the Notepad prefetch file being read in the context of the Notepad process during its startup. Lines 7–19 (which have time stamps 10 seconds later than the first four lines) show the SuperFetch service—running in the context of a Svchost process—writing out the updated prefetch file.

To minimize even further, every three days or during system idle periods, the SuperFetch service organizes a list of files and directories in the order that are referenced during a boot or application start and stores them in a file named %SystemRoot\Prefetch\Layout.ini (see Figure 5-34). This list includes frequently accessed files tracked by SuperFetch.

![](bbox=[0.125, 0.283, 0.473, 0.583])

**Figure 5-34** Prefetch defragmentation layout.

It launches the system defragmenter with a command-line option that tells the defragmenter to defagment based on the contents of the file instead of performing a full defragment. The defragmenter finds a contiguous area on each volume large enough to hold all the listed files and directories that reside on that volume and moves them in their entirety into that area so they are stored one after the other. Thus, future prefetching operations will be more efficient because all the data is now stored physically on the disk in the order it will be. Because the files defragmented for prefetching usually only number in the hundreds, this defragmentation is much faster than full-volume defragmentations.

# Placement policy

When a read receives a page, the memory manager must determine whether in physical memory to put the virtual page. The set of rules it uses to determine the best position is called a placement policy. Windows considers the size of CPU memory caches when choosing page frames to minimize unnecessary thrashing of the cache.