start with Csr). Ntdll.dll also includes run-time library routines (functions that start with Rt1), support for user-debugging (functions that start with DbgUi), Event Tracing for Windows (functions starting in Etw), and the user-mode asynchronous procedure call (APC) dispatcher and exception dispatcher. APCs are explained briefly in Chapter 6 and in more detail in Chapter 8 Part 2, as well as exceptions.

Finally, you'll find a small subset of the C Run-Time (CRT) routines in Ntdll.dll, limited to those that are part of the string and standard libraries (such as memory, strcpy, sprintf; and so on); these are useful for native applications, described.

# Native images

Some images (executables) do not link to any subsystem. In other words, they don't link against a set of subsystem DLLs, as Kernel32.dll for the Windows subsystem. Instead, they link to Ntdll.dll, which is the lowest common denominator that spans subsystems. Because the native API exposed by Ntdll.dll is mostly documented, these kind of images are typically built only by Microsoft. One is the Session Manager process (Smss.exe, described in more detail later in this chapter). Smss.exe is the first user-mode process created (by the kernel), so it cannot be dependent on the Windows subsystem Csrss.exe (the Windows subsystem process) has not started. In fact, Smss.exe is responsible for launching Csrss.exe another example is the Autoch utility which sometimes runs at startup to check disks. Because it relatively early in the boot process (launched by Smss.exe, in fact), it cannot depend on any subsystem.

Here is a screenshot of Smss.exe in Dependency Walker, showing its dependency on Ntdll.dll. Notice the subsystem is indicated by Native.

![](bbox=[0.125, 0.542, 0.875, 0.683])

# Executive

The Windows is the upper layer of Ntoskrnl.exe (The kernel is the lower layer). The executive includes the following types of functions:

+   * Functions that are exported and called from user mode These functions are called system services and are exported via Ntdll.dll (such as NtCreateFile from the previous experiment). Most of the services are accessible through the Windows API or the APIs of any environment subsystem. A few services, however, aren't available through any documented subsystem function (Examples include ALPC and various query functions such as NtQueryInformationProcess, specialized functions such as NtCreateOpenFile, and so on).