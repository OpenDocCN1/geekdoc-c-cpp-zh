
| Device | Type |
| :--- | :--- |
| 854fb50 Device | KMDF0 |
| 95bb040 Device | ProcessManagement |
| 97ad9fe0 SymbolicLink | MailslotRedirect |
| 84f0090 Device | 0000036 |
| 84c6538 Device | FakeVid5 |
| 8bf14e98 Device | Video1 |
| 8bf2fe20 Device | KeyboardClass1 |
| 89c32a0 Device | 0000029 |
| 89c05030 Device | Vol1grControl |
| 89c3a1a Device | VMBus |

When you enter the object command and specify an object manager directory object, the kernel debugger dumps the contents of the driver according to how the object manager organizes it internally. For fast lookups, a directory stores objects in a hash table with a hash of the object names, so the output shows the objects stored in each bucket of the directory's hash table.

As Figure 6-10 illustrates, a device object points back to its driver object, which is how the I/O manager driver routine calls when it receives an I/O request. It uses the device object to find the driver object representing the driver that services the device. It then indexes into the driver object by the function code supplied in the original request. Each function code corresponds to a driver entry point (called a dispatch routine).

A driver object often has multiple device objects associated with it. When a driver is unloaded from the system, the I/O manager uses the queue of device objects to determine which devices will be affected by the removal of the driver.

## EXPERIMENT: Displaying driver and device objects

You can display driver and device objects with the !devobj and !devobj kernel debugger commands. In the following example, the driver object for the keyboard class driver is examined, and one of its device objects:

```
1: kd> !devobj kbdclass
Driver object (8a557520) is for:
\Driver\kbdclass
Driver Extension List: (id , addr)

Device Object list:
9f509648 8bf2fe20 8a541030
1: kd> !devobj
Device object (9f509648) is:
KeyboardClass2 \Driver\kbdclass DriverObject 8a557520
nCurrent Irp 00000000 Count 0 0000000b Flags 00000244
dacl 82090960 DevExt 9f509700 DevExt 9f5097f0
ExtensionFlags (0x00000c00) DOE_SESSION_DEVICE, DOE_DEFAULT_PRESENT
Characteristics (0x00001000) FILE_DEVICE_SECURE_OPEN
AttachedTo(Lower) 9F509848 \Driver\internpt
Device is not busy.

Notice that the drobj command also shows you the addresses and names of any device objects that object you're viewing is layered (the AttachedTo line). It can also show the device objects layered on top of the object specified (the AttachedDevice line), although not in this case.

The drobj command can accept an optional argument that indicates more information to show. Here is an example with the most information to show:

```
1: kd> drobj kbclass 7
Driver object (8a5572d0) is for:
\Driver\kbclass
 Extension List: (id , addr)

Device Object list:
9F509648 8b2fe20 8a541030
```

| Field | Address |
| :--- | :--- |
| DriverEntry | 8c30a10 |
| DriverStartTo | 00000000 |
| DriverLoad | 00000000 kbdclass!KeyboardAddDevice |
| AddDevice: | 8c307250 |

| Dispatch routines | Address |
| :--- | :--- |
| [00] MJ_CREATE | 8c301d80 kbdclass!KeyboardClassCreate |
| [01] MJ_CREATE_NAMED_PIPE | 81a42342 nt!InvalidDeviceRequest |
| [02] MJ_CLOSE | 8c30c190 kbdclass!KeyboardClassClose |
| [03] MJ_READ | 8c302150 kbdclass!KeyboardClassRead |
| [04] MJ_WRITE | 81a42342 nt!InvalidDeviceRequest |
| [05] MJ_QUERY_INFORMATION | 81a42342 nt!InvalidDeviceRequest |
| [06] MJ_SET_INFORMATION | 81a42342 nt!InvalidDeviceRequest |
| [07] MJ_QUERY_EA | 81a42342 nt!InvalidDeviceRequest |
| [08] MJ_SET_EA | 8c30a10 kbdclass!KeyboardClassFlush |
| [09] MJ_FLUSH_BUFFERS | 8c306768 nt!InvalidDeviceRequest |
| [10] MJ_QUERY_VOLUME_INFORMATION | 81a42342 nt!InvalidDeviceRequest |
| [11] MJ_SET_VOLUME_INFORMATION | 81a42342 nt!InvalidDeviceRequest |
| [12] MJ_DIRECTORY_CONTROL | 81a42342 nt!InvalidDeviceRequest |
| [13] MJ_SYSTEM_CONTROL | 81a42342 nt!InvalidDeviceRequest |
| [14] MJ_DEVICE | 8c3076d0 kbdclass!KeyboardDevice |

| Control | Address |
| :--- | :--- |
| [09] MJ_INTERNAL_DEVICE_CONTROL | 8c30ff70 kbdclass!KeyboardPass |
| [10] MJ_SHUTDOWN | 81a42342 nt!InvalidDeviceRequest |
| [11] MJ_LOCK_CONTROL | 81a42342 nt!InvalidDeviceRequest |
| [12] MJ_CLEANUP | 8c302260 kbdclass!KeyboardClassCleanup |
| [13] MJ_CREATE_SLOT | 81a42342 nt!InvalidDeviceRequest |
| [14] MJ_QUERY_SECURITY | 81a42342 nt!InvalidDeviceRequest |
| [15] MJ_SET_SECURITY | 81a42342 nt!InvalidDeviceRequest |
| [16] MJ_POWER | 8c301440 kbdclass!KeyboardClassPower |
| [17] MJ_SYSTEM_CONTROL | 8c307f40 kbdclass!KeyboardClassSystem |
| [18] IRP_DEVICE_CHANGE | 81a42342 nt!InvalidDeviceRequest |
| [19] IRP_QUERY_VOLUME | 81a42342 nt!InvalidDeviceRequest |
| [1a] IRP_SET_VOLUME | 81a42342 nt!InvalidDeviceRequest |
| [1b] IRP_MJ_PNP | 8c301870 kbdclass!KeyboardPnP |

The dispatch routines are clearly shown, and will be discussed in the next section. Note that operations not supported by the driver are passed to the I/O manager’s routine. The address to the !devobj command is for a DRIVER_OBJECT, and the address for the !devobj command is a DEVICE_OBJECT. You can view these structures directly using the debugger.

```
1: kd nt!_driver_object 8a557520
+0000 Type : 4
+0002 Size : 0x168
+0004 DeviceObject : 0x9f509648 _DEVICE_OBJECT
+0008 Flags : 0x412
+00c0 DriverStart : 0xc30000 Void
+0010 DriverSize : 0x000
+0014 DriverSection : 0x8a557c8 _DRIVER_EXTENSION
+0018 DriverExtension : 0x8a557c8 _
+001c DriverName : _UNICODE_STRING "kbdclass"
+0024 Hardware_database : 0x815c2c28 _UNICODE_STRING "REGISTRY_MACHINE\DESCRIPTION\SYSTEM"
+0028 FastIoDispatch : (null)
+002c DriverInit : 0x8c30a10 long +ffffffff8c30a10
+0030 DriverStart : (null)
+0034 DriverUnload : (null)
+0038 MajorFunction : [28] 0x8c301d80 long +ffffffff8c301d80
1: kd nt!_device_object 9f509648
+0000 Type : 3
+0002 Size : 0xa18
+0004 ReferenceCount : 0x8557520 _DRIVER_OBJECT
+0008 DriverObject : 0xbf2fe20 _DEVICE_OBJECT
+000c NextDevice : (null)
+0010 AttachedDevice : (null)
+0014 CurrentIrp : (null)
+0018 Timer : (null)
+001c Flags : 0x2044
+0020 Characteristics : 0x100
+0024 Vpb : (null)
+0028 DeviceExtension : 0x9f509700 Void
+002c DeviceType : (null)
+0030 StackSize : 7
+0034 Queue : <unnamed-tag>
+005c AlignmentRequirement : 0
+0060 DeviceQueue : _KDEVICE_QUEUE
+0074 Dpc : _KPC
+0094 ActiveThreadCount : 0
+0098 SecurityDescriptor : 0x82099030 Void
```

There are some interesting fields in these structures, which will be discussed in the next.

Using objects to record information about drivers means that the I/O manager doesn't need to know details about individual drivers. The I/O manager merely follows a pointer to a driver, providing a layer of portability and allowing new drivers to be easily loaded.

## Opening devices

A file object is a kernel-mode data structure that represents a handle to a device. File objects clearly fit the criteria for objects in Windows: They are system resources that two or more processes can share; they have names; they are protected by object-security; and they support synchronization. File objects provide a memory-based representation of resources that can be read from or written to. Table 6-1 lists the file object's attributes.

| Attribute | Purpose |
| :--- | :--- |
| File name | This identifies the file that the file object refers to, which was passed in CreateFile or CreateFile2. |
| Current byte offset | This identifies the location in the file (valid only for synchronous I/O). |
| Share modes | These indicate whether other callers can open the file for read, write, or delete while the current caller is using it. |
| Open mode flags | These indicate whether I/O will be synchronous or asynchronous, cached or non-sequential, random and so on. |
| Pointer to device object | This identifies the type of device the file resides on. |
| Pointer to the volume block (VPB) | This identifies the volume, or partition, that the file resides (in the case of file system). |
| Pointer to section object pointers | This is a root structure that describes a mapped/cached file. This structure also contains the cache map, which identifies which parts of the file are cached (or mapped) by the cache manager and where they reside in the cache. |
| Pointer to private cache map | This is used to store per-page caching information for this handle or the page priority for the process. See Chapter 5, "Memory management," for information on page priority. |
| List of I/O request packets (IRPs) | If thread-I/O (described in the section "Thread-asynchronous I/O" later in this chapter) and the file object is associated with a completion part (described in the section "I/O completion ports") this is a list of all the operations that are associated with this file. |
| I/O completion context | This is context information for the current I/O completion part, if one exists. |
| File object extension | This stores the I/O priority (explained later in this chapter) for the file and whether share-access checks should be performed on the file object, and contains optional file extensions that store context-specific information. |

To maintain some level of opacity toward driver code that uses the file object, and allow extending without enlarging the file functionality, the structure also contains an extension field, which allows up to six different kinds of additional attributes, described in Table 6-2.
