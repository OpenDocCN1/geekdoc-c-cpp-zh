
# Microsoft Windows

2000 (NT 5.0), Windows XP (NT 5.1), Windows Server 2003 (NT 5.2), Windows Vista (NT 6.0), and Windows 7 (NT 6.1).

The Microsoft XBOX and XBOX 360 also run a variant of NT, forked from Windows 2000. Most future Microsoft operating system products are based on NT in some shape or form.

# 4.3 Virtual Memory

32 bit WinNT allows for a maximum of 4Gb of virtual memory space, divided into ‘pages' that are 4096 bytes by default. Pages not in use by the system or any of the applications may be written to a special section on the harddisk known as the ‘paging file.’ Use of the paging file may increase performance on some systems, although high latency for I/O to the HDD can actually reduce performance in some instances.

# 4.4 System Architecture

The Windows architecture is heavily layered. Function calls that a programmer makes be redirected 3 times or before any action is actually performed. There is an unignorable penalty for calling Win32 functions from a user-mode application. However, the upside is equally unignorable: code written in higher levels of the Windows system is easier to write. Complex operations that involve initializing multiple data structures and calling multiple sub-functions can be performed by calling a single higher-level function.

The Win32 API calls 3 modules: KERNEL, USER, and GDI KERNEL functions are layered on top of NTDLL, and most calls to KERNEL are simply redirected into NTDLL calls. USER and GDI are both based on Win32K (a kernel-mode module, responsible for the Windows ‘look and feel’), although USER also makes calls to the more-primitive functions in GDI. This and NTDLL both provide an interface to the Windows NT kernel, NTOSRNL (see further).

NTOSRNL is also partially layered on HAL (Hardware Abstraction Layer), but this interaction will not be considered in this. The purpose of this layering is to allow processor variant issues (such as location of resources) to be separate from the actual kernel itself. A slightly different system configuration thus requires just a different HAL module, rather than a completely different kernel.

# 4.5 System calls and interrupts

After filtering different layers of subroutines, most API calls require interaction with part of the operating system. Services are provided via ‘software interrupts’, the traditionally through the ‘int 0x2e’ instruction. This switches control of execution to the NT executive / kernel, where the request is handled. It should be pointed out that the stack used in kernel mode is different from the user mode stack. This provides an added layer of protection between kernel and user. Once the function completes, control is returned back to the user application.

Both Intel and AMD provide an extra set of instructions to allow faster system calls, the 'SYSENTER' instruction from Intel and the SYSCALL instruction from AMD.

# 4.6 Win32 API

Both WinNT and Win9x systems utilize the Win32 API. However, the WinNT version of the API has more functionality and security constructs, as well as Unicode support. Most of the Win32 API can be broken down into 3 separate components, each performing a separate task.

# 4.6.1 kernel32.dll

Kernel32.dll, home of the KERNEL subsystem, is where non-graphical functions are implemented. The Heap API, the Virtual Memory API, File I/O API, the Thread API, the System Object Manager, and other system services. Most of the functionality of kernel32.dll is implemented in ntdll.dll, but undocumented functions. Microsoft prefers to publish documentation for kernel32 and guarantee that these APIs will remain unchanged, and then most of the work in other libraries, which are then not documented.

# 4.6.2 gdi32.dll

gdi32.dll is the library that implements the GDI system, where primitive graphical operations are performed. GDI diverts most of its calls into WIN32K, but it does contain a manager for GDI objects, such as pens, brushes and device contexts. The GDI object manager and the KERNEL object manager are completely separate.

# 4.6.3 user32.dll

The USER subsystem is located in the user32.dll library file. This subsystem controls the creation and manipulation of USER objects, which are common screen items such as windows, menus, cursors... USER set up the objects to be drawn, but will perform the actual drawing by calling on GDI (which in turn will make calls to WIN32K) or sometimes calling WIN32K directly. USER utilizes the GDI Object Manager.

# 4.7 Native API

The native API, hereby referred to as the NTDLL subsystem, is a series of undocumented API function calls that handle most of the work performed by KERNEL. Microsoft also does not guarantee that the native API will remain the same between different versions, Microsoft Developers modify the software. This gives the risk of native API calls being removed or changed without warning, breaking software that utilizes it.

# 4.7.1 ntdll.dll

The NTDLL subsystem is located in ntdll.dll. This library contains many API function calls, all which follow a particular naming scheme. Each function has a prefix: Ldr, Nt, Zw, Csr, etc., and all of the functions that have a particular prefix follow all particular rules.

The 'official' native API is usually limited to functions whose prefix is Nt or Zw.

- Ldr: stands for Load Library
- Nt: stands for Native
- Zw: stands for Windows
- Csr: stands for Client Server Runtime
- Dbg: stands for Debug
- Rtl: stands for Run Time
- Memory Management: stands for Memory Management-- Thread: stands for Thread Management
- Object: stands for Object Management
- System: stands for System Management
- DLL: stands for DLL
- Kernel: stands for Kernel
- User: stands for User
- GDI: stands for Graphics Device Interface
- HAL: stands for Hardware Abstraction Layer
- NTOSRNL: stands for NT Operating System Loader

# 4.7.2 User Mode Versus Kernel Mode

Many of the native API functions are exported in kernel-mode. It is important to note that the format of many of the calls are identical in Win32 and Win64, except for the size of pointers, and other data types that are specific to 64-bit address space.

# 4.8 ntoskrnl.exe

This module is the Windows "Executive", which sits on the lower-level, more primitive NTOSRNL. It is responsible for maintaining the state of the operating system.

# 4.9 Win32K.sys

This module is the "Win32 Kernel" that sits on top of the NT executive. WIN32K is responsible for the "look and feel" of windows. many portions of this code have remained largely unchanged since the Win9x versions. This module is responsible for translating the API calls from USER and GDI into the pictures you see on the monitor.

# 4.10 Win64 API

With the advent of 64-bit processors, 64-bit software is a necessity. As a result, the Win64 API was created to utilize the new hardware. It is important to note that the format of many of the functions are identical in Win32 and Win64, except for the size of pointers and other data types.

# 4.10.1 Differences

Microsoft has released a new version of its Windows operating system, named "Windows Vista." Vista may be better known by its development code-name "Longhorn." Microsoft claims that Vista has been written largely from the ground up, and therefore it can be assumed that there are fundamental differences between the Vista API and system architecture, and the APIs and architectures of previous Windows versions. Windows Vista was released January 30, 2007.

# 4.12 Windows CE/Mobile, and other versions

Windows CE is the Microsoft offering on small devices. It largely uses the same Win32 API as the desktop systems, although it has a slightly different architecture.

# 4.13 "Non-Executable Memory"

Recent windows of service packs have attempted to implement a system known as "Non-executable memory" where certain pages can be marked as "non-executable". The purpose of this system is to prevent some of the most common security holes by not allowing control to pass code inserted into a memory buffer by an attacker.
