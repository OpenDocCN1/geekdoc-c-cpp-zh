repeated relocations. As such, a library that supports ASLR has loaded once at a given address, it will always be loaded at that same address. This also means that the relevant bitmap sets have been calculated for the functions in that library, which will be identical in all other processes that load the same binary. As such, the memory manager treats the CFG bitmap as a region of pagefile-backed shareable memory, and the physical pages that correspond to the shared bits only exist in RAM once.

This reduces the cost of the committed pages in RAM and that only the bits corresponding to private copy-on-write memory. In regular applications, private memory is not executable unless someone has patched a library (which will not happen at image load), so the cost of loading an application, if it shares libraries with as previously launched applications, is nil met. The next experiment demonstrates this.

# EXPERIMENT: Control Flow guard bitmap

Open the VMap tool and select a Notepad. You should see a large reserved block in the Sharable section like so:

![](bbox=[0.138, 0.381, 0.706, 0.731])

You can lower the base by size and quickly locate the large chunk for the CFGBmap, as shown. Additionally, if you want to process and use the !address command on the process, you will use WinDbg debugging the CFG bitmap:

+   + 7df6'ff530000 7df6'0118a000 01'c5a000 MEM_MAPPED_MEM_RESERVE
Other [CFG. Bitmap]
+ 7df6'0118a000 7df6'011fb000 00007100 MEM_MAPPED_MEM_COMMIT_PAGE_NOACCESS
Other [CFG. Bitmap]
+ 7df6'011fb000 7df6'ff530000 1ff'de335000 MEM_MAPPED_MEM_RESERVE
Other [CFG. Bitmap]

746 CHAPTER 7 Security