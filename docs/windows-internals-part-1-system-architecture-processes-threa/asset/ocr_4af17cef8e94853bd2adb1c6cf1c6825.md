+   - For sizes less than or equal to 128 KB (and not serviced by the LFH), the VS allocator uses: Both VS and LFH allocators use the back end to create the required heap sub-segments as necessary.

+   - Allocations larger than 128 KB and less than equal to 500 KB are serviced directly by the heap back end.

+   - Allocations larger than 508 KB are serviced by calling the memory manager directly (Virtual-A11oc) since these are so large that the default 64 KB allocation granularity (and rounding to the nearest page size) is deemed good enough.

Here is a quick comparison of the two heap implementations:

+   - In some scenarios, the segment heap may be somewhat slower than the NT heap. However, it's likely that future Windows versions would make it on par with the NT heap.

+   - The segment heap has a lower memory footprint for its metadata, making it better suited for low-memory devices such as phones.

+   - The segment heap's metadata is separated from the actual data, while the NT heap's metadata is interspersed with the data itself. This makes the segment heap more secure, as it's more difficult to get the metadata of an allocation given just a block address.

+   - The segment heap can be used only for a growable heap. It cannot be used with a user-supplied memory mapped file. If such a segment heap creation is attempted, an NT heap is created instead.

+   - Both heaps support LFH-type allocations, but their internal implementation is completely different. The segment heap has a more efficient implementation in terms of memory consumption and performance.

As mentioned, UWP apps use segment heaps by default. This is mainly because of their lower memory footprint, which is suitable for low-memory devices. It is also used with certain system processes based on executable: csrss.exe, lsass.exe, runtimebroker.exe, smss.exe, and svchost.exe.

The segment heap is not the default heap for desktop apps because there are compatibility concerns that may affect existing applications. It is likely in future versions, it will become the default. To enable or disable the segment heap for a specific executable, you can set an Image File Execution Options value named EndHeapDebugOpts (DWORD):

+   - Bit 2 (4) to disable segment heap

+   - Bit 3 (8) to enable segment heap

You can globally enable or disable the segment heap by adding a value named Enabled (DWORD) to the HKLM\SYSTEM\CurrentControlSet\Session Manager\Segment Heap registry key. A zero value disables the segment heap and a non-zero value enables it.