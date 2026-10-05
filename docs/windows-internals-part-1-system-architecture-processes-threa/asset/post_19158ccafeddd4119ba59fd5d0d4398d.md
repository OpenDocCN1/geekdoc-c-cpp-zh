
Because user-mode processes running in VTL 1 are isolated, potentially malicious code—while not able to exert influence over the system—attempt system calls (which would allow it to seal/sign its own secrets), and potentially cause bad interactions with other VTL 1 processes or the smart kernel. As such, only a special class of specially signed binaries, called Trustlets, are allowed to execute in VTL 1. Each Trustlet has a unique identifier and signature, and the secure kernel has hard-coded knowledge of which Trustlets have been created so far. As such, it is possible to create Trustlets without the secure kernel (which only Microsoft can touch), and existing Trustlets cannot be patched in any way (which would require the special Microsoft Signature). For information on Trustlets, see Chapter 3.

The addition of the secure kernel and VBS is an exciting step in modern OS architecture. With additional hardware changes to various buses as PCI and USB, it will soon be possible to support an entire class of secure devices, which, when combined with a minimalistic HAL, secure Plug-and-Play manager, and secure User-Mode Device Framework, could allow VTL 1 applications to access specially designated devices, such as for biometric or smartcard input. New versions of Windows 10 are likely to leverage these advances.

## System key components

Now we've looked at the high-level architecture of Windows, let's delve deeper into the internal structure and the role each OS component part plays. Figure 2-4 is a more detailed and complete diagram of the core Windows system architecture and components than shown in Figure 2-1. Note that it still does not show all components (networking in particular, which is explained in Chapter 10, "Networking," in Part 2).

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_77_0.png)

Figure 2-4 Windows architecture.

The following sections elaborate on each major element of this diagram. Chapter 8 in Part 2 explains the primary control mechanisms the system uses (such as the object manager, interrupts, and so forth). Chapter 11, “Startup and shutdown,” in Part 2 describes the process of starting and shutting down Windows, and Chapter 9 in Part 2 details management mechanisms such as the registry, service processes and WMI. Other chapters explore in more detail the internal structure and operation of key areas such as processes and memory management, the i/o manager, storage management, the cache manager, the Windows file system (NTFS), and networking.

## Environment subsystems and subsystem DLLs

The role of an environment subsystem is to expose some subset of the base Executive system services to application programs. Each subsystem can provide access to different subsets of the native services in Programs. That means some things can be done from an application built on one subsystem that can't be done by an application built on another subsystem. For example, a Windows application can't use the SUA function.

Each executable (.exe) is bound to one and only one subsystem. When an image is run, the process creation code examines the subsystem code in the header so that it can notify the proper subsystem of the new type. This code is specified with the /SUBSYSTEM linker option (or the SubSystem entry in the Linker/System property page of the project's properties).

As mentioned, applications do not call Windows DLLs directly. Instead, they go through one or more subsystems which export the documented interface that the programs linked to that subsystem can call. For example, the Windows subsystems (such as Kernel32.dll, Advapi32.dll, User32.dll, and Gdi32.dll) implement the Windows API functions. The SUA subsystem (pssdll.dll) is used to implement the API functions (on Windows versions that supported POSIX).

> EXPERIMENT: Viewing the image subsystem

You can see the image subsystem by using the Dependency tool (Depends.exe). For example, note the image types for two different images: Notepad.exe (the simple text editor) and Cmd.exe (the Windows command prompt):

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_78_0.png)

| Module | File Stamp | Link Time | File Size | Alt | Link Checksum | Checksum | CPU | Symbols |
|---|---|---|---|---|---|---|---|---|
| NTDLL.DLL | 1992-09-15 14:36:50 | 1992-09-16 11:40:53 | 142,956 | A | 0x0001C79A | 0x0001C79A | x64 | Console | CV:Unknown |
| ADVAPI32.DLL | 1992-09-15 14:36:50 | 1992-09-16 11:40:53 | 74,656 | A | 0x0001B18A | 0x0001B18A | x64 | Console | CV:Unknown |
| GDI32.DLL | 1992-09-15 14:36:50 | 1992-09-16 11:40:53 | 68,168 | A | 0x0001E443 | 0x0001E443 | x64 | Console | CV:Unknown |
| USER32.DLL | 1992-09-15 14:36:50 | 1992-09-16 11:41:34 | 510,464 | A | 0x0001D333 | 0x0001D333 | x64 | Console | CV:Unknown |
| NSDI.DLL | 1992-09-15 14:36:50 | 1992-09-16 11:23:48 | 20,138 | A | 0x0000C0D1 | 0x0000C0D1 | x64 | Console | CV:Unknown |
| NTDLL.DLL | 1992-09-15 14:36:50 | 1992-09-16 11:28:22 | 1,855,900 | A | 0x0001D070 | 0x0001D070 | x64 | Console | CV:Unknown |
