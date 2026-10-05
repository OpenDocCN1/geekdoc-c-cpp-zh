You can use Device Manager on your machine to see what is occupying the various reserved memory regions that cannot be used by Windows (and that will show up as holes in MemInfo's output). To check Device Manager, follow these steps:

+   1. Run Devmgmt.msc.

+   2. Open the View menu and select Resources by Connection.

+   3. Expand the Memory node. On the laptop used for the output shown in Figure 5-43, the primary consumer of mapped device memory is unsurprisingly, the video card (Hyper-V S3 Cap), in the range F8000000-FFFFFFFF.

![](bbox=[0.215, 0.255, 0.485, 0.423])

**FIGURE 5-43** Hardware-reserved memory on a 32-bit Windows system.

Other miscellaneous devices account for most of the rest, and the PCI bus reserves additional devices for devices as part of the conservative estimation the firmware uses during boot.

# Memory compression

The Windows 10 memory managers implement a mechanism that compresses private and page-file-backed section pages that are modified on the manager page list. The primary candidates for compression are private pages belonging to UWP apps because compression works well with the working set swapping and emptying that occurs for such applications if memory is tight. After an application is suspended its working set can be emptied at any time and dirty pages can be compressed. This will create additional available memory that may be enough to hold another application in memory without making the first application's pages leave memory.

> Note Experiments have shown that pages compress to around 30–50 percent of their original size using Microsoft’s Xpress algorithm, which balances speed with size, thus resulting in considerable memory savings.

The memory compression architecture must adhere to the following requirements:

+   A page cannot be in a compressed and an uncompressed form because this would waste physical memory due to duplication. This means that whenever a page is compressed, it must become a free page after successful compression.