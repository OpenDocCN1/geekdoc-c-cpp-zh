# Section objects

As noted earlier in this chapter in the “Shared memory and mapped files” section, the section object, which the Windows subsystem calls a *file mapping object*, represents a block of memory that two or more processes can share. A section object can be mapped to the paging file or to another file on

The executive uses sections to load executables into memory, and the cache manager uses to access data in a cached file (See Chapter 14 in Part 2 for more information on how the cache manager uses section objects). You can also use section objects to map a file into a process address space. The file can then be accessed as a large array by mapping different views of the section object and reading or writing to memory rather than the file—an activity called mapped file I/O. When the program accesses an invalid page (one not in physical memory), a page fault occurs and the memory manager automatically brings the page into memory from the mapped file or page file. If the application modifies the page, the memory manager writes the changes back to the file during its normal operations. Alternatively, the application can flush a file explicitly by using the Windows FlushFile function().

Like other objects, section objects are allocated and deallocated by the object manager. The object manager creates and initializes an object header, which uses to manage objects; the memory manager defines the body of the section object (See Chapter 8 in Part 2 for more on the object manager). The memory manager also implements services that user-mode threads can retrieve and change the attributes stored in the body of section objects. The structure of a section object is shown in Figure 5-31. Table 5-14 summarizes the unique attributes stored in section objects.

| | Section |
|---||
| Object body attributes | Maximum Size, Page Protection, Paging File or Mapped Based or Not Based |
| Services | Create Section, Open Section, Extend Section, Map/Unmap View, Query Section |

**FIGURE 5-31** A section object.

**TABLE 5-14** Section object body attributes

| Attribute | Purpose |
|---|---|
| Maximum size | This is the largest size to which the section can grow in bytes. If mapping a file, this is the maximum size of the file. |
| Page protection | This is page-based memory protection assigned to all pages in the section when it is created. |
| Paging file or mapped file | This indicates whether the section is created empty (backed by the paging file—as explained earlier, file-backed sections use page file resources only when the pages need to be written out to disk) or backed by a file (backed by the mapped file). |
| Based or not based | This indicates whether a section is a based section, which must appear at the same virtual address for all processes, or a non-based section, which can be accessed at different virtual addresses for different processes.

CHAPTER 5 Memory management 405