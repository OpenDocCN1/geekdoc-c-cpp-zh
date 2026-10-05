![](bbox=[0.125, 0.056, 0.663, 0.279])

FIGURE 5-4 The "before" of copy-on-write.

If a either process writes to a page, a memory-management fault is generated. The memory manager sees that the write is to a copy-on-write page, so instead of reporting the fault as an access violation, it does the following:

+   1. It allocates a new read/write page in physical memory.
2. It copies the contents of the original page to the new page.
3. It updates the corresponding page-mapping information (explained later in this chapter) in this process to point to the new location.
4. It dismisses the exception, causing the instruction that generated the fault to be re-executed.

This time the write operation succeeds. However, as shown in Figure 5-5, the newly copied page is now private to the process that did the writing and isn't visible to the other process sharing the copy-on-write page. Each new process that writes to that shared page will also get its own private copy.

![](bbox=[0.125, 0.626, 0.663, 0.846])

FIGURE 5-5 The "after" of copy-on-write.

One application of copy-on-write is to implement breakpoint support in debuggers. For example, by default, code pages start out as execute-only. If a programmer sets a breakpoint while debugging