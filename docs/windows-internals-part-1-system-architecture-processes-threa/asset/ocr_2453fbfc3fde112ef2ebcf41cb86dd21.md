![](bbox=[0.166, 0.058, 0.37, 0.301])

**FIGURE 16** Spinlock acquisition.

When synchronizing at IRQL 2—for example, between a dispatch routine and a DPC or between a DPC and another DPC (running on another CPU, of course)—the kernel provides the KeAcquireSpinLock and ReleaseSpinLock functions (there are other variations that are discussed in Chapter 8 of Part 2). These functions perform the steps in Figure 6-17 where the “associated IRQL” is 2. The driver in this case must allocate a spinlock (KSPIN_LOCK, which is just 4 bytes on 32-bit systems and 8 bytes on 64-bit systems), typically in the device extension (where driver-managed data for the device is kept) and initialize it with InitializeSpinLock.

For synchronizing with any function (such as DPC), different interrupts must be used. Every interrupt object (KINTERRUPT) holds inside a spinlock, which is acquired before the ISR executes (this implies that the ISR cannot run concurrently on other CPUs). Synchronization in this case would be with spinlock (no need to allocate another one), which can be acquired indirectly with the KeInterruptSpinLock function and with ReleaseInterruptSpinLock. Another option is to use the KeSynchronizeExecution function, which accepts a callback function driver that is called between the acquisition and release of the interrupt spinlock.

By now, you should realize that although ISRs require special attention, data that a device driver uses is subject to being accessed by the same device driver (one of its functions) running on another processor. Therefore, it’s critical for device-driver code to synchronize its use of any global or shared data or access to the physical device itself.

# I/O requests to layered drivers

The “IRP flow” section showed the general options drivers have for dealing with IRPs, with a focus on a standard WDM device node. The preceding section showed how an I/O request to a simple device controlled by a single device driver is handled. I/O processing for file-based devices or for requests to other layered drivers happens in the same way, but it’s worthwhile to take a closer look at the request targeted at file-system drivers. Figure 6-18 shows a very illustrative example of how an asynchronous I/O request might travel through layered drivers for non-hardware based devices as primary targets. It uses as an example a disk controlled by a file system.

CHAPTER 6 I/O system 533