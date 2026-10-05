• The zero page thread (MiZeroPageThread, priority 0) This zeroes out the page list so that a cache of zero pages is available to satisfy demand-zero page faults. In some cases, memory zeroing is by a faster function MiZeroInParallel1. See the note in the “Page list dynamics” section later in this chapter.

Each of these components is covered in more detail later in the chapter except for the segment dereference thread, which is covered in Chapter 14, Cache manager,” in Part 2.

# # Large and small pages

Memory management is done in distinct chunks called pages. This is because the hardware management unit translates virtual to physical addresses at the granularity of page. Hence, a page is the smallest unit of protection at the hardware level. (The various page-protection options are described in the section “Protecting memory” later in this chapter.) The processors on Windows support two page sizes: small and large. The actual sizes vary based on the processor architecture, and they are listed in Table 5-1.

TABLE 5-1 Page sizes
| Architecture | Small Page Size | Large Page Size | Small Pages per Large Page |
|---|---|---|--|
| x86 (PAE) | 4 KB | 2 MB | 512 |
| x64 | 4 KB | 2 MB | 512 |
| ARM | 4 KB | 4 MB | 1024 |

> Note Some processors support configurable page sizes, but Windows does not use this feature.

The primary advantage of large pages is speed of address translation for references to data within the large page. This advantage exists because the first reference to any byte within a large page will cause the hardware’s translation look-aside buffer (TLB) (described in the section “Address translation” later in this chapter), to have in cache the information necessary to translate to any other byte within the large page. If small pages are used, more TLB entries are needed for the same range of virtual addresses, increasing the recycling of entries. In turn, this means to go back to the page tables when references are made to virtual addresses outside the scope of a small page whose translation has changed. The TLB is a very small cache; large pages make better use of this limited resource.

To take advantage of large pages on systems with more than 2 GB of RAM, Windows maps with large pages the core operating system images (Ntoskrnl.exe and Hal) as well as core system data (such as the part of non-paged pool and the data structures that describe the state of each physical memory). Windows automatically maps I/O space (by MmMapIoSpace) with large pages if the request is of a satisfactorily large page length and alignment. In addition, Windows allows applications to map their images, private memory, and page