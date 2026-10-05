# Page priority

Every physical page in the system has a page priority value assigned to it the memory manager. The page priority is a number in the range 0 to 7. Its main purpose is to determine the order in which pages are consumed from the standby list. The memory manager divides the standby list into eight sublists that each stores pages of a particular priority. When the memory manager wants to take a page from the standby list, it takes pages from low-priority lists first.

Each thread and process in the system is also assigned a page priority. A page priority usually reflects the page priority of the thread that causes its allocation. (If the page is shared, it reflects the highest page priority among the sharing threads.) A thread inherits its page-priority value from the process to which it belongs. The memory manager uses lower priorities for pages it reads from disk speculatively when anticipating a process's memory accesses.

By default, processes use a page-priority value of 5, but the SetProcessInformation and SetThreadInformation use functions to change process and thread priority values. These functions call the NetSetInformationProcess and NetSetInformation-Thread functions. You can look at the memory priority of a thread with Process Explorer (per-page priority can be displayed by looking at the PFN entries, which you will see later in the chapter). Figure 5-38 shows Process Explorer's threads tab information about Winlog's memory. Although the thread priority is high, the standard is 5.

![](bbox=[0.125, 0.465, 0.465, 0.815])

**Figure 5-38** Process Explorer's threads tab.

The real power of memory priorities is realized only when the relative priorities of pages are under- at a high level, which is the role of PrefFetch, covered at the end of this chapter.