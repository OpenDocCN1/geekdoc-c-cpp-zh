
to the existing system page tables when a process is created. If the process is part of a session, session space page tables are also shared by pointing the session space page directory entries to the existing session page tables.

## Page tables and page table entries

PDE points to a page table. A page table is a simple array of PTEs. Too, so, a PDPT. Every page table has 512 entries and each PTE maps a single page (4 KB). This means a page table can map a 2 MB address space (512 x 4 KB). Similarly, a page directory has 512 entries, each pointing to a page table. This means a page directory can map 512 x 2 MB or 1 GB of address space. This makes sense because there are four PDPs, which can map the entire 32-bit kernel space.

For large pages, the PDE points with 11 bits to the start of a large page in physical memory, the byte offset is taken for the lower 21 bits of the original virtual address. This means a large page does not point to any page table.

The layout of a page directory and page table is essentially the same. You can use the kernel debugger /pte command to examine PTEs. (See the upcoming experiment “Translating addresses.”) We’ll discuss valid PTEs here and invalid PTEs in the section “Page fault handling.” Valid PTE have two main fields: the PFN of the physical page containing the data or the physical address of a page in memory, and some flags that describe the state and protection of the page. (See Figure 5-18).

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_391_0.png)

FIGURE 5-18 Valid x86 PTEs.

The bits labeled “Software” and “Reserved” in Figure 5-18 are ignored by the memory management unit (MMU) inside the CPU regardless of whether the PTE is valid. These bits are stored and interpreted by the memory manager. Table 5-10 briefly describes the hardware-defined bits in a valid PTE.

## TABLE 5-10 PTE status and protection bits

| Name of Bit | Meaning |
| :--- | :--- |
| Accessed | The page has been accessed. |
| Cache disabled | This disables CPU caching for that page. |
| Copy-on-write | The page is using copy-on-write (described earlier). |
| Dirty | The page has been written to. |
| Global | Translation applies to all processes. For example, a translation buffer flush won't affect this PTE. |
| Large page | This indicates that the PDE maps a 2 MB page. (Refer to the section "Large and small pages" earlier in this chapter) |
| No execute | This indicates that code cannot execute the page. (It can be used for data only.) |
| Owner | This indicates whether user-mode code can access the page or whether the page is limited to kernel-mode access. |
| Prototype | The PTE is a prototype PTE, which is used as a template to describe shared memory associated with section objects. |
| Valid | This indicates whether the translation maps to a page in physical memory. |
| Write through | This marks the page as write-through or, if the processor supports the page attribute table, write-combined. This is typically used to map video buffer memory. |
| Write | This indicates to the MMU whether the page is writable |

On x86 systems, a hardware PTE contains two bits that can be changed by the MMU: the dirty and accessed bit. The MMU sets the accessed bit whenever the page is read or written (provided it is not already set). The MMU sets the dirty bit whenever a write operation occurs over the page. The operating system is responsible for clearing these bits at the appropriate times. They are never cleared by the MMU.

The x86 MMU uses a bit to provide page protection. When this bit is clear, the page is read-only. When it is set, the page is read/write. If a thread attempts to write to a page with the bit clear, a memory-management exception occurs. In addition, the memory manager's access handler (described later in the section "Page fault handling") must determine whether the thread is allowed to write to the page (for example, if the page was marked copy-on-write) or whether an access violation should be generated.

## Hardware versus software write bits in page table entries

The additional bit implemented in software (refer to Table 5-10) is used to force an update of the dirty bit to be synchronized with Windows memory management data. In a simple implementation, the memory manager would set the hardware write bit (bit 1) for any writable page. A write to any page will cause the MMU to set the dirty bit in the PTE. The dirty bit will tell the memory manager that the contents of that physical page must be written to store before the physical page can be used for something else.

In practice, in multiprocessor systems, this can lead to race conditions that are expensive to resolve. At any time, the MMUs of various processors can set the dirty bit of any PTE that has its write bit set. The memory manager, at various times, update the working set to reflect the state of the dirty bit in a PTE. The memory manager uses a lock to synchronize access to the working set. But in a multiprocessor system, even while one processor is holding the lock, the dirty bit might be changed by MMUs of other CPUs. This raises the possibility of missing an update to a dirty bit.

To avoid this, the Windows memory manager initializes read-only and writable pages with the hardware write bit (bit 1) of their PTEs set to 0 and records the true writable state of the page in the software write bit (bit 11). On the first access to such a page, the processor will raise a memory-management exception because the hardware write bit is clear, just as it would be for a read-only page. In this case, though, the memory manager learns that the page is actually writable (via the software write bit), acquires the working set pushlock, sets the dirty bit and updates the working set list to note that the page has changed, releases the working set pushlock, and dismisses the exception. The hardware write operation then proceeds as usual, but the setting of the dirty bit is made to happen with the working set pushlock.

On subsequent writes to the page, no exceptions occur because the hardware write bit is set. The MMU will redundantly set the dirty bit, but this is benign because the "written-to" state of the page is already recorded in the working set list. The first write to a page to go through this exception may seem to be excessive overhead. However, it happens only once per writable page as long as the page remains valid. Furthermore, the first access to almost any page already goes through memory-management exception because usually in the invalid state (the PTE bit 0 is clear). If the first access is also the first page, the dirty handling just described will occur within the handling of the first-access fault, the additional overhead is small. Finally, on uniprocessor and multiprocessor systems, this implementation allows flushing of the translation look-aside buffer (described in the next section) without holding a lock for each page flushed.

## Translation look-aside buffer

As you've learned, each hardware address translation requires three lookups:

- One to find the right entry in the PDPT
- One to find the right entry in the page directory (which provides the location of the page table)
- One to find the right entry in the page table

Because three additional memory lookups for every reference to a virtual address would quadruple the required bandwidth to memory, resulting in poor performance, all CPUs cache address translations so that repeated accesses of the same addresses have to be repeatedly translated. This cache is an array of associative memory called the translation lookahead buffer (TLB). Associative memory is a vector whose cells can be read simultaneously and compared to a target value. In the case of the TLB, the vector contains the virtual-to-physical page mappings of the most recently used pages, as shown in Figure 5-19, and the type of page protection, size, attributes, and so on applied to each page. Each entry in the TLB is like a cache entry whose holds portions of the virtual address and whose data portion holds a physical page number, protection field, valid bit, and usually a dirty bit indicating the condition of the page to which the cached PTE corresponds. If a PTE's global bit is set (as is done by Windows for system space pages that are visible to all processes), the TLB entry isn't invalidated on process switches.
