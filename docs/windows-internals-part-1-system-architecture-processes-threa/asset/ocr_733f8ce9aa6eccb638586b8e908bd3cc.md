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

When you enter the object command and specify an object manager directory object, the kernel debugger dumps the contents of the driver according to the object manager organizes it internally. For fast lookups, a directory stores objects in a hash table with a hash of the object names, so the output shows the objects stored in each bucket of the directory's hash table.

As Figure 6-10 illustrates, a device object points back to its driver object, which is how the I/O manager driver routine calls when it receives an I/O request. It uses the device object to find the driver object representing the driver that services the device. It then indexes into the driver object by the function code supplied in the original request. Each function code corresponds to a driver entry point (called a dispatch routine).

A driver object often has multiple device objects associated with it. When a driver is unloaded from the system, the I/O manager uses the queue of device objects to determine which devices will be affected by the removal of the driver.

# EXPERIMENT: Displaying driver and device objects

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
```