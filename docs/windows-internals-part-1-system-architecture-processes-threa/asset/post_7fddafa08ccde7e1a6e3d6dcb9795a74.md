
# Commit charge and the system commit limit

We are now in a position to thoroughly discuss the concepts of commit charge and the system commit limit.

Whenever virtual address space is created—for example, by a VirtualAlloc call (for committed memory) or MapViewOfFile call—the system must ensure that there is room to store it, either in RAM or in backing store, before successfully completing the request. For mapped memory or other sections mapped to the page file, the file associated with the mapping object referenced by the MapViewOfFile call provides the required backing store. All other virtual allocations on system-managed shared resources for storage: RAM and the paging file)(to track all uses of these resources to ensure they are never overcommitted—that is, there is no more virtual address space defined than there space to store its contents, either in RAM or in backing store (disk).

This section makes frequent references to paging files. It is possible (though not recommended) to run Windows without any paging files. Essentially, this means that when RAM is exhausted, there is no room to grow and memory allocations, generating a blue screen. You can consider every reference to paging files here to be qualified by “if one or more paging files exist.”

Conceptually, the system commit limit represents the total committed virtual address space that can be created in addition to virtual allocations that are associated with their backing store—that, in addition to sections mapped to files. Its numeric value is simply the amount of RAM available to Windows plus the current sizes of any page file. If a page file is expanded or new page files are created, the commit limit increases accordingly. If no page files exist, the system commit limit is simply the total amount of RAM available to Windows.

Commit charge is the system-wide total of all committed memory allocations that must be kept in either RAM or in a paging file. From this it should be apparent that any contributor to commit charge is private-committed virtual address space. However, there are many other contributors, some of them not obvious.

Windows also maintains a per-process counter called the process page file quota. Many of the allocations that contribute to commit charge also contribute to the process page file quota. Note, however, this does not represent each process’s private contribution to the system commit charge. It represents the potential or maximum page file usage, should these allocations have to be stored.

The following types of memory allocations contribute to the system commit charge and, in many cases, to the process file quota.(Some of these will be described in later sections of this chapter).

- Private committed memory: This is memory allocated with the VirtualAlloc call with the MEM_COMMIT option. This is the most common type of contributor to the commit charge. These allocations are also charged to the process page file quota.
- Page-file-backed mapped memory: This is allocated with a MapViewOfFile call that references a section object, which in turn is not associated with a file. The system uses a portion of the page file as the backing store inside. These allocations are not charged to the process file quota.
- Copy-on-write regions of mapped memory (even if it is associated with ordinary mapped files): The mapped file provides backing store for its own unmodified content. However, should a page in the copy-on-write region be modified, it can no longer use the original mapped file for backing store. It must be kept in RAM or in a paging file. These allocations are not charged to process quota.
- Non-paged and paging pool allocations in system space that are not backed by explicitly associated files: Even the free regions of the system pools contribute to charge. The non-paged regions are counted in the commit charge though they will never be written to the page file because they reduce the amount of RAM available for private data.
- Kernel stacks: Threads’ executing in kernel mode.
- Page tables: Most of these are themselves pagable and are not backed by mapped files. However, if they are not pagable, they occupy RAM. Therefore, the space required for them contributes to commit charge.
- Space for page tables that are not yet allocated: As you will see, large areas of virtual space have been defined but not referenced (example, private virtual space), the system need not actually create page tables to describe it. However, the space for these-yet-nonexistent page tables is charged to commit charge to ensure that the page tables can be created when needed.
- Allocations of physical memory via APIs discussed previously consume physical memory directly. For many of these items, the commit charge may represent the potential use of storage rather than its actual use. For example, a page of private committed memory does not actually occupy RAM or the equivalent page file until it is referenced. But commit charge accounts for pages when the virtual space is first created ensures there will be private storage later.

A particularly interesting case occurs when reserving virtual memory and committing it. When the reserved region is created with VirtualAlloc, system commit is not charged for the actual virtual region. On Windows 8 and Server 2012 and earlier versions, page table hierarchies will be required to describe the region, even though these might not yet exist or be eventually needed. Starting with Windows 8 and Server 2012 R2, page tables for reserved regions are not charged immediately; this means huge memory regions can be allocated without exhausting pages. This becomes important in some security features, such as Guard (see Chapter 7 for more details). If the region or a part of it is later committed, system memory is charged to account for the size of the region (and page tables), as the process file quota.

Another, when the system successfully completes, for example, a VirtualAlloc call or MapView, it makes a commitment that the necessary storage will be available when needed, if it wasn't needed at that moment. Thus, a later memory reference to the allocated region can never fail for lack of storage space. (Of course, it could still fail for other reasons, as page protection, the region being deallocated, and so on.) The commit charge mechanism allows the system to keep this commitment.

The commit charge appears in Performance Monitor counters as Memory: Committed Bytes. It is also the first of the two numbers displayed on the Task Manager’s Performance tab with the Commit (second being the commit limit), and it is displayed by Process Explorer’s System Information tab as Commit Charge — Current.

The process file quota appears in the performance counters as Process: Page File Bytes. The same data appears in Process Private bytes counter. (Neither exactly describes the true meaning of the counter)

If the commit charge reaches the commit limit, the memory manager will attempt to increase the commit limit by expanding one or more page files. If that is not possible, subsequent attempts to allocate virtual memory that commit charge will fail until some committed memory is freed. The counters listed in Table 5-13 allow you to examine private committed memory usage on a system-wide, per-process, or per-page-file, basis.

**TABLE 5-13** Committed charge and page file performance counters

| Performance Counter | Description |
| :--- | :--- |
| Memory: Committed Bytes | This is the number of bytes of virtual (not reserved) memory that has been committed. This memory doesn't necessarily represent page file usage because it includes committed pages in physical memory that have never been paged out. Rather, it represents the charge that must be paid by page file space and/or RAM. |
| Memory: Commit Limit | This is the number of bytes of virtual memory that can be committed without having to extend the paging files. If the paging files can be extended, this limit is soft. |
| Process: Page File Quota | This is the process's contribution to Memory: Committed Bytes. |
| Process: Private Bytes | This is the same as Process: Page File Quota. |
| Process: Working Set — Private | This is the subset of Process that is currently in RAM and can be referenced without a page fault. |
| Process: Working Set | This is the subset of Virtual Bytes that are currently in RAM and can be referenced without a page fault. |
| Process: Virtual Bytes | This is the total virtual memory allocation of the process, including mapped regions, private committed regions, and reserved regions. |
| Paging File: % Usage | This is the percentage of the page file space that is currently in use. |
| Paging File: % Usage Peak | This is the highest observed value of Paging File: % Usage. |
