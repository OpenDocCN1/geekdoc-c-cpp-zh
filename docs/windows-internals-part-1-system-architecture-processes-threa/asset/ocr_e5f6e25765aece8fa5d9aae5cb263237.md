+   - Enable free checking A free block is filled with a pattern that is created at various points when the heap manager needs to access the block, such as at removal from the free list to satisfy allocate request. If the process continues to write to the block after freeing it, the heap manager will detect changes in the pattern and the error will be reported.

+   - Parameter checking This function consists of extensive checking of the parameters passed to the heap functions.

+   - Heap validation The entire heap is validated at each heap call.

+   - Heap tagging and stack traces support This function supports the specification of tags for allocation/or captures user-mode stack traces for the heap calls to help narrow the possible causes of a heap error.

The first three options are enabled by default if the loader detects that a process is started under the control of a debugger (a debugger can override this behavior and turn off these features.). You can specify the debugging features for an executable image by setting various debugging flags in the header using the Gflags tool (See the next example and the section "Windows flags" in Chapter 8 in Part 2). Alternatively, you can enable heap debugging using the !heap command in the standard Windows debuggers. (See the debugger help for more information.)

Enabling heap-debugging options affects all heaps in the process. Also, if any of the heap-debugging options are enabled, the LFH will be disabled automatically and the core heap will be used (with the required debugging options enabled). The LFH is not used for heaps that are not expandable (because of the extra overhead added to the existing heap structures) or for heaps that do not allow serialization.

# # Pageheap

Because the tail and free checking options described in the preceding sections might discover corruptions that occurred before the problem was detected, an additional heap debugging capability, called pageheap, is provided. Pageheap directs all or part of the heap calls to a different heap manager. You can enable pageheap using the Gflags tool (part of the Debugging Tools for Windows). When enabled, the heap manager places allocations at the end of pages and reserves the page that immediately follows. Because reserved pages are not accessible, a buffer overflow that will cause an access violation, making it easier to detect the offending code. Optionally, pageheap allows for the placement of blocks at the beginning of the pages, with the preceding reserved page, to detect overrun problems (a rare occurrence). Pageheap can also protect free pages against any access to detect references to heaps after they have been freed.

Note that using pageheap can cause you to run out of address space (in 32-bit processes) because of the significant overhead added for small allocations. Also, performance can suffer due to the increase of references to demand zero pages, loss of locality, and additional overhead caused by frequent calls to validate heap structures. A process can reduce the impact by specifying that the page-heap be used only for blocks of certain sizes, address ranges, and/or originating DLLs.