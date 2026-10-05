consumption by individual devices are handled by device drivers but are coordinated by the power manager and PoFx. On certain classes of devices, the terminal timeout manager also manages physical display timeouts based on device usage and proximity.

+   **Windows Driver Model (WDM) Windows Management Instrumentation (WMI)** These routines, discussed in Chapter 9 in Part 2, enable device drivers to publish performance and configuration information and receive commands from the user-mode WMI service. Consumers of WMI information can be on the local machine or remote across the network.

+   **Memory manager** The memory manager, discussed in Chapter 5, implements virtual memory, a memory management scheme that provides a large private address space for each process that can exceed available memory. The memory manager also provides the underlying support for the cache manager. It is assisted by the prefetcher and Store Manager, also explained in Chapter 5.

+   **Cache manager** The cache manager, discussed in Chapter 14, "Cache manager," in Part 2, improves the performance of file-based I/O by causing recently referenced disk data to reside in main memory for quick access. It also achieves this by deferring writes by holding the updates in memory for a short time before sending them to the disk. As you'll see, it does this by using the memory manager's supported pools.

In addition, the executive contains four main groups of functions that are used by the executive components listed above. About three of these support functions are documented in the WDK because drivers also use them. These are the four categories of support functions:

+   **Object manager** The object manager creates, manages, and deletes Windows objects and abstract data types that are used to represent OS resources as processes, threads, and the various synchronization objects. The object manager is explained in Chapter 8 in Part 2.

+   **Asynchronous LPC (ALPC) facility** The ALPC facility, explained in Chapter 8 in Part 2, passes messages between a client process and a server process on the same computer. Other things, ALPC is used as a local transport for remote procedure call (RPC), the Windows implementation of an industry-standard communication facility for client and server processes across a network.

+   **Run-time library functions** These include string processing, arithmetic operations, data type conversion, and security structure processing.

+   **Executive support routines** These system use memory allocation (paged and non-paged pool), interlocked memory access, as well as special types of synchronization mechanisms such as executive resources, fast mutexes, and pushlocks.

The executive also contains a variety of other infrastructure routines, which of some are mentioned briefly in this book:

+   **Kernel debugger library** This allows debugging of the kernel by a debugger supporting KD, a portable protocol supported over a variety of transports such as USB, Ethernet, and IEEE 1394, and implemented by WinDbg and the Kd.exe debuggers.