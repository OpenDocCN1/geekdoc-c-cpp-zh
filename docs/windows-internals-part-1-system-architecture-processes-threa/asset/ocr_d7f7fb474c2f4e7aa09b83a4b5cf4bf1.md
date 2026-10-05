As the feature is still officially in beta at the time of this writing and subject to significant change, won't cover the actual internals of the subsystem in this book. We will, however, take another look at Pico processes in Chapter 3. When the subsystem matures beyond you, you will probably see official documentation on MSDN and stable APIs for interacting with Linux processes from Windows.

# Ntdll.dll

Ntdll.dll is a special system support library primarily for use of subsystem DLLs and native applications. (*Native in this context refers to images that are not tied to any particular subsystem.) It contains two types of functions:

+   - System service dispatch stubs to Windows executive system services

+   - Internal functions used by subsystems, subsystem DLLs, and other native functions

The first group of functions provides the interface to the Windows executive system services that can be called from user mode. There are more than 450 functions, such as NtCreateFile, NtSetEvent, and so on. As noted, most of the functions are accessible through the Windows API. (A number are not, however, and are for use only by specific OS-internal processes)

For each of these, Ntdll.dll contains an entry point with the same name. The code function contains the architecture-specific instruction that causes a transition into kernel to invoke the system service dispatcher. (This is explained in more detail in Chapter 8 in Part 2.) After verifying some parameters, this system service dispatcher calls the actual kernel-mode system service that contains the real code inside Ntoskrnl.exe. The following experiment shows what these functions look like.

# EXPERIMENT: Viewing the system dispatcher code

Open the version of WinDbg that corresponds to your architecture (for example the x64 version on 64 bit Windows). Then open the File menu and select Open Executable. Navigate to %SystemRoot%System32 and select Notepad.exe.

Notepad should launch and the debugger should be in the initial breakpoint. This is very early in the life of the process, which you can witness by executing the k (call) command. You should see a few functions starting with Ldr, which indicates the loader state. The main function for Notepad has not executed yet, which you won't see in Notepad's window.

Set a breakpoint in the NtCreateFile inside Ntdll.dll (the debuggers are not sensitive):

```
bp ntdll!NtCreateFile
```

Enter the g (command) or press FS to let Notepad continue execution. The debugger should break almost immediately, showing something like this (x64):

```
Breakpoint 0 hit
tdll!NtCreateFile
0007ffa9f4eb10 4c8bd1	mov r10,rcx
```