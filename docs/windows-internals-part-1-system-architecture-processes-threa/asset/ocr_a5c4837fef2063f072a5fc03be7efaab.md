Note The I/O priority in the IRP and/or file object is a hint. There is no guarantee that the I/O priority will be respected or even supported by the different drivers that are part of the storage stack.

The prioritization strategies are implemented by two different types of drivers. The hierarchy is implemented by the storage drivers, which are responsible for all I/Os on a specific port, such as ATA, SCSI, or USB. The ATA port driver (Atatop.sys) and USB port driver (Ubsport.sys) implement this strategy, while the SCSI and storage port drivers (Sciport.sys and Storport.sys) do not.

Note All port drivers check specifically for Critical I/Os and move ahead of their queues, even if they do not support the full hierarchy mechanism. This mechanism is in place to support critical memory paging I/Os to ensure system reliability.

This means that consumer mass storage devices as IDE or SATA drives and USB flash disks will take advantage of I/O prioritization, while devices based on SCSI, Fibre Channel, and iSCSI will not.

On the other hand, it is the system class device driver (Classpnp.sys) that enforces the idle strategy, so it automatically applies to I/Os directed at all devices, including SCSI drives. This separation ensures that idle I/O be subject to back-off algorithms to ensure a reliable system during operation under high idle I/O usage and that applications that use them can make forward progress. Placing support for this strategy in the Microsoft-provided class driver avoids performance problems that would have been caused by lack of support for it in legacy-party port drivers.

Figure 6-27 displays a simplified view of the storage stack that shows where each strategy is implemented. Chapter 12 in Part 2 for more information on the storage stack.

![](bbox=[0.128, 0.616, 0.563, 0.858])

FIGURE 6-27 Implementation of I/O prioritization across the storage stack.