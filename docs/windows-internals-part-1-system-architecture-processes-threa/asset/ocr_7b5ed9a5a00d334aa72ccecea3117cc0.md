routine can change or disappear if the current operation is not cancelled. If a thread that issues an I/O request before the operation is completed or the operation is cancelled (for example, the CancelIo or CancelIoEx functions), the I/O manager executes the IRP's cancel routine if it is assigned to it. A cancel routine is necessary to release any resources acquired during the processing that has already taken place for the IRP as well as for completing the IRP with a canceled status.

+   **Fast-dispatch routines** Drivers that use the cache manager, such as file-system drivers, typically provide these routines to the kernel to bypass typical I/O processing when accessing the driver. (See Chapter 14, "Cache manager," in Part 2, for more information on the cache manager). Operations, such as reading or writing can be quickly performed by accessing the cache data directly instead of taking the I/O manager's usual path that generates discrete I/O operations. Fast dispatch routines are also used as a mechanism for callbacks from the memory manager and cache manager to file-system drivers. For instance, when creating a section, the memory manager calls back into the file-system driver to acquire the file exclusively.

+   **An unload routine** An unload routine releases any system resources in use so that the I/O manager can remove the driver from memory. Any resources acquired in the initialization routine (DriverEntry) are usually released in the unload routine. A driver can be loaded and unloaded while the system is running if the driver supports it, but the unload routine will be called only after all files to the device are closed.

+   **A system shutdown notification routine** This routine allows driver cleanup on system shutdown.

+   **Error-logging routines** When unexpected errors occur (for example, when a disk block goes bad), a driver's error-logging routines note the occurrence and notify the I/O manager. The I/O manager writes this information to an error log file.

# Driver objects and device objects

When a thread opens a handle to a file object (described in the "I/O processing" section later in this chapter), the I/O manager must determine the file name which driver it should call to process the request. Furthermore, the I/O manager must be able to locate the information the next time ahead uses the same file handler. The following system objects fill this need:

+   **A driver object** This represents an individual driver in the system (DRIVER_OBJECT structure). The I/O manager obtains the address of each of the driver's dispatch routines (entry points) from the driver object.

+   **A device object** This represents a physical or logical device on the system and describes its characteristics (DEVICE_OBJECT structure), such as the alignment requirements for buffers and the location of its device queue to hold incoming IRPs. It is the target for all I/O operations because this object is what the hardware communicates with.

The I/O manager creates a driver object when a driver is loaded into the system. It calls the driver's initialization routine (DriverEntry), which fills in the object attributes with the driver's entry points.