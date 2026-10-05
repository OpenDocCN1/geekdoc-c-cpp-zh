
In most cases, lower-level filter drivers modify the behavior of hardware driver. For example, if a device reports to its bus that it requires 4 I/O ports when it actually requires 16 I/O ports, a lower-level, device-specific function filter driver could intercept the list of hardware resources reported by the bus to the PnP manager and update the count of I/O ports.

Upper-level PnP drivers usually provide added-value features for a device. For example, an upper-level device filter driver for a disk can enforce additional security checks.

Interrupt processing is explained in Chapter 8 in Part 2 and in the narrow context of device drivers, in Chapter 6. Further details about the I/O manager, WDM, Plug and Play, and power management are also covered in Chapter 6.

# Windows Driver Foundation

The Windows Driver Foundation (WDF) simplifies Windows driver development by providing two frameworks: the Kernel-Mode Driver Framework (KMDF) and the User-Mode Driver Framework (UMDF). Developers can use KMDF to write drivers for Windows 2000 SP4 and, while UMDF supports Windows XP and later.

KMDF provides a simple interface to WDM and hides its complexity from the driver without modifying the underlying bus/function/filter model. KMDF drivers respond to events that they can register and call into the KMDF library to perform work that is not specific to the hardware they are managing, such as generic power management or synchronization.(Previously, each driver had to implement this in its own). In some cases, more than 200 lines of WDM code can be replaced by a single KMDF function call.

UMDF enables classes of drivers—mostly USB-based or other high-latency protocol buses, such as those for video cameras, MP3 players, cell phones, and printers—to be implemented as usermode drivers. UMDF runs each user-mode driver in what is essentially a user-mode service, and it uses ALPC to communicate with a kernel-mode wrapper driver that provides actual access to hardware. If a UMDF driver crashes, the process dies and restarts. That way, the system doesn't become unstable, while the service hosting the driver restarts.

UMDF has two major versions: version 1.x is for all OS versions that support UMDF, the last and best being version 1.1. This version uses C++ and COM for driver writing, which is more convenient for user-mode programmers, but it makes the UMDF different from KMDF. Version 2.0 of UMDF, introduced in Windows 8, is based on the same object model as KMDF, making the two frameworks very similar in their programming model. Finally, WDF has been open-sourced by Microsoft, and at the time of this writing is available on GitHub https://github.com/Microsoft/Windows-Driver-Frameworks.

# Universal Windows drivers

With Windows 10, the Universal Windows drivers refer to the ability to write device drivers once that APIs and Device Driver Interfaces (DDIs) provided by the Windows 10 common core. These drivers are binary-compatible for a specific CPU architecture (x86, ARM) and are used on a variety of form factors, for IoT devices, to phones, to the HolLens and Xbox One, to laptops and desktops. Universal drivers can use KDF, UMDF 2.x, or WDM as their driver model.

# EXPERIMENT: Viewing the installed drivers

To list the installed drivers, run the System Information tool (Msinfo32.exe). To launch this tool, click Start and then run Msinfo32 to locate it. Under System, expand Software Environment and open System Drivers. Here's an example output of the list of installed drivers:

| System Name | Name | Description | File | Type | Started | Start Mode | State |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Hardware Resources | Jware | 1394 CHCI Compliant Co... | c:\windows\ | Kernel | No | Manual | Stopped |
| Software Environment | Jware | Microsoft API Driver | c:\windows\ | Kernel | Yes | Boot | Running |
| System Drivers | acpi | Microsoft API Driver | c:\windows\ | Kernel | Yes | Boot | Running |
| Print Jobs | acpi | ACPI Processor Aggregator D... | c:\windows\ | Kernel | No | Manual | Stopped |
| Network Connections | acptime | ACPI Wake Alarm Driver | c:\windows\ | Kernel | No | Manual | Stopped |
| Loaded Modules | amd640 | Intel API Bus Filter | | Kernel | No | Manual | Stopped |
| Services | ammidlang | Auxiliary Function for Wil... | c:\windows\ | Kernel | Yes | System | Running |
| Program Groups | ammidlang | Application Package Caching... | c:\windows\ | Kernel | No | System | Running |
| Windows Error Repo | ammidlang | AMD KB Processor Driver | c:\windows\ | Kernel | No | Manual | Stopped |
| | ammidlang | AMD PCI Processor Driver | | Kernel | Yes | Boot | Running |
| | amdmmpfd | AMD PCI Root Lower Filter | c:\windows\ | Kernel | No | Manual | Stopped |
| | amdsulta | AMD Processor Driver | | Kernel | No | Manual | Stopped |
| | amdbcs | amdbca | | Kernel | No | Manual | Stopped |
| | appfilterservice | appid | Apps Touch Pad Filter fo... | c:\windows\ | Kernel | Yes | Manual | Running |
| | asvraid | Adapter for SATA/SAS/9 RAID Stor... | c:\windows\ | Kernel | No | Manual | Stopped |

This window displays list of device drivers defined in the registry, their type, and state (Running or Stopped). Device drivers and Windows processes are both defined in the same place: HKLM\SYSTEM\CurrentControlSet\Services. However, they are distinguished by a type code. For example, type 1 is a kernel-mode driver. For a complete list of the information stored in the registry, see Chapter 9 in Part 2.

Alternatively, you can list the currently loaded device drivers by selecting the System process in Process Explorer and opening the DLL view. Here's a sample output. (To get the extra columns, right-click a header and Select Columns to see all the available modules for modules in the DLL tab.)

CHAPTER 2 System architecture 85

# Peering into undocumented interfaces

Examining the names of the exported or global interfaces in system kernel (such as Nkrnl, Hal, or Ntdll.dll) can be enlightening—you get into the idea of things Windows can do what happens to be documented and supported today. Of course, just because you know the names of these functions means that you can or call them—the interfaces are undocumented and are subject to change. We suggest that you look at them.

CHAPTER 2 System architecture 86

# TABLE 2-5 Commonly Used Prefixes

| Prefix | Component |
| :--- | :--- |
| Alpc | Advanced Local Procedure Calls |
| Cc | Common Cache |
| Cm | Configuration manager |
| Dbg | Kernel debug support |
| Dbgk | Debugging Framework for user mode |
| Em | Errata manager |
| Etw | Event Tracing for Windows |
| Ex | Executive support routines |
| FsRtl | File System Runtime Library |
| Hv | Hive library |
| Hvl | Hypervisor library |
| Io | I/O manager |
| Kd | Kernel debugger |
| Ke | Kernel |
| Kse | Kernel Shim Engine |
| Lsa | Local Security Authority |
| Mm | Memory manager |
| Nt | NT system services (accessible from user mode through system calls) |
| Ob | Object manager |
| Pf | Prefetcher |
| Po | Power manager |
| Pof | Power framework |
| Pp | PnP manager |
| Ppm | Processor power manager |
| Ps | Process support |
| Rtl | Run-time library |
| Se | Security Reference Monitor |
| Sm | Store manager |
| Tm | Transaction manager |
| Ttm | Terminal timeout manager |
| Vf | Driver Verifier |

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_102_0.png)
