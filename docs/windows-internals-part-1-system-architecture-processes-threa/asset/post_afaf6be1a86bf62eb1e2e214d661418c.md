
object passed to the I/O manager. This option also monitors IRPs to ensure drivers mark them correctly when completing them asynchronously, that they manage device-stack locations correctly, and in addition, the Verifier randomly pokes drivers by sending them power management and WMI IRPs, the order in which devices are enumerated, and adjusting the status of PnP and power IRPs when they complete to test drivers that return incorrect dispatch routines. Finally, the Verifier also detects re-initialization of remove locks while they are still being held due to pending device removal.

- **DMA Checking** is a hardware-supported mechanism that allows devices to transfer data to memory without involving the CPU. The I/O manager provides several functions that drivers use to initiate and control DMA operations, and this option enables checks for the correct use of the functions and buffers that the I/O manager supplies DMA operations.

- **Force Pending I/O Requests** For many devices, asynchronous I/Os completes immediately, so drivers may not be coded to handle the occasional asynchronous I/O. When this option is enabled, the I/O manager returns STATUS_PENDING in response to a driver's calls to IoCallDriver, which simulates the asynchronous completion of an I/O.

- **IRP Logging** This monitors a driver's use of IRPs and makes a record of usage, which is stored in WMI information. You can then use the Dc2wmipparser.exe utility in the WDK to convert these WMI records to a text file. Note that only 20 IRPs for each device will be recorded—each subsequent IRP will overwrite the last recently added entry. After a reboot, this information is discarded, so Dc2wmipparser.exe should be run if the contents of the trace are to be analyzed.

## Memory-related verification options

The following are memory-related verification options supported by Driver Verifier. (Some are related to I/O operations.)

## Special Pool

Selecting the Special Pool option causes the pool routines to bracket pool allocations with an invalid page before or after the allocation will result in a kernel-mode access violation, crashing the system with the finger pointed at the buggy driver. Special pool also causes some additional validation checks to be performed when a driver allocates or frees memory. For special pool, the pool allocation routes a region of kernel memory for Driver Verifier use. Driver Verifier redirects memory allocation requests that drivers under verification to the special pool area rather than the standard kernel-mode pools. When a device allocates memory from special pool, Driver Verifier rounds the allocation up to an even-page boundary. Because Driver Verifier brackets the allocated page with invalid pages, if a device driver attempts to read or write the end of the buffer, the driver will access an invalid page, and the memory manager will raise a kernel-mode access violation.

Figure 6–31 shows an example of the special pool buffer that Driver Verifier allocates to a device driver when Driver Verifier checks for overrun errors.

| Invalid Page | Page 2 (High Address) |
| :--- | :--- |
| Driver Buffer | Page 1 |
| Random Data | |
| Invalid Page | Page 0 (Low Address) |

**FIGURE 6-31** Layout of special pool allocations.

By default, Driver Verifier performs overrun detection. It does this by placing buffer that the device driver uses at the end of the allocated page and filling the beginning of the page with a random pattern. Although the Driver Verifier Manager doesn't let you specify overrun detection, you can set this type of detection manually by adding the DWORD registry value PoolTagOverruns to the HKLM\SYSTEM\CurrentSet\Control\SessionManager\Memory key and setting it to 0 (or by running the Glfgags.exe utility and selecting the **Verify Start** option in the Special Pool Tag section of the default option, Verify End). When Windows enforces overrun detection, Driver Verifier allocates the driver's buffer at the beginning of the page rather than at end.

The overrun-detection configuration includes some measure of overrun detection as well. When the driver frees its buffer to return the memory to Driver Verifier, Driver Verifier ensures that the preceding buffer hasn't changed. If the pattern is modified, the driver has overun the buffer and writes to memory outside the buffer.

Special pool allocations also check to ensure that the processor IRQL at the time of allocation and deallocation is legal. This check catches an error that some drivers make: allocating pageable memory from IRQL at DPC/dispatch level or above.

You can also configure special pool manually by adding the DWORD registry value PoolTag in the HKLM\SYSTEM\CurrentSet\Control\SessionManager\Memory key, which represents the allocation tags used for special pool. Thus, even if Driver Verifier isn't configured to verify a particular device, if the driver associates with memory it allocates what is specified in the PoolTag registry value, the pool routines will allocate the memory from special pool. If you set the PoolTag value to 0x2a or the wildcard (*), all memory that allocate will be from special pool, provided there's enough virtual and physical memory (drivers will revert to regular pool if there aren't enough free pages).

## Pool tracking

If pool tracking is enabled, the memory manager checks at driver load time whether the driver freed all the memory it allocated. If it didn't, it crashes the system, indicating the buggy driver. Driver Verifier also shows general statistics on the Driver Verifier Manager's Pool Tracking tab (accessible from the main wizard UI by selecting **Display Information About the Currently Verified Drivers** and selecting Next. You can also use the Verifier kernel debug command. This shows more information than Driver Verifier and is used by writer drivers.

Pool tracking and special pool cover not only explicit allocation calls, such as ExAllocatePoolWith-Tag, but also calls to other kernel APIs that implicitly allocate memory from: IoAllocatePoolMd, IoAllocateIrp, and other IRP allocation calls; various Rt1 APIs; and IoSetCompletionRoutine.

Another verifier function enabled by the Pool Tracking option returns to pool quota charges. The call to ExAllocatePoolWithQuotaTag charges the current process quota for the number of bytes allocated. If such a call is made from a DPC routine, the process that is charged is unpredictable because DPC routines may execute in the context of any process. The Pool Tracking option checks for calls to this routine from the DPC routine context.

Driver Verifier can also perform locked memory tracking, which checks for pages that have been locked after an I/O operation and generates a DRIVER_LEFT_LOCKED_PAGES_IN_PROCESS crash instead of PROCESS_HAS_LOCKED_PAGES—the former indicates the driver responsible for the error as well as the function for protection of the pages.

## IRQL Checking

One of the most common device driver bugs occurs when a device driver is executing at an elevated IRQL. The memory manager can't service a page fault when the IRQL is DPC/dispatch level or above. The system doesn't detect instances of a device driver accessing passable data when the processor is executing at a high IRQL level because the passable data happens to be physically resident at the time. At other times, the data might be paged out, which results in a system crash with the code IRQL_NOT_LESS_OR_EQUAL (that is, the IRQL wasn't less or equal to the level required for the operation attempted—in this case, accessing memory).

Testing device drivers for this kind of bug is usually difficult, Driver Verifier makes it easy. If you select the IRQL Checking option, Driver Verifier forces all kernel-mode passable code and data out of the system working when a device driver raises the IRQL. The internal function that does this is MiAllocateSystemMemory. With this setting, whenever a device driver accesses passable memory when the IRQL is elevated, the system detects the violation, and the resulting crash identifies the faulty driver.

Another common driver crash results from incorrect IRQL usage when synchronization objects are part of data structures that are paged and then waited. Synchronization objects are never paged because the dispatcher needs to access them at an elevated IRQL, which would cause a crash. Driver Verifier checks whether any of the following structures are present in passable memory: KTIMER, KMUTEX, KSPIN_LOCK, KEVENT, KSEMAPHORE, ERESOURCE, and FAST_MUTEX.

## Low Resources Simulation

Enabling Low Resources causes Driver Verifier to randomly fail memory allocations that verified device drivers perform. In the past, developers wrote many device drivers under the assumption that kernel memory would always be available, and if memory ran out, the device driver-
