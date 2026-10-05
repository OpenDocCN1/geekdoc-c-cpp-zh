13. The application and command-line arguments passed to CreateProcessInternalW are analyzed. The executable path name is converted to the NT name (for example, c:\temp\a.exe turns into something \device\harddiskvolume\temp\a.exe) because some functions require it in that format.

14. Most of the gathered information is converted into a large structure of type RTL_USER_PROCESS_PARAMETERS.

Once these steps are completed, CreateProcessInternalW performs the initial call to NtCreateUserProcess to attempt creation of the process. Because Kernel32.dll has no image at this point whether the application image name is a real Windows application or a batch file (.bat or .cmd), 16-bit, or DOS application, the call might fail, at point CreateProcessInternalW looks at the error reason and attempts to correct the situation.

# Stage 2: Opening the image to be executed

At this point, the creating thread has switched into kernel mode and continues the work within the NtCreateUserProcess system implementation.

+   1. NtCreateUserProcess validates first arguments and builds an internal structure to hold all creation information. The reason for validating arguments again is to make sure the call to the executive did not originate from a hack that managed to simulate the Ntdll.dll makes the transition to the kernel with bogus or malicious arguments.
2. As illustrated in Figure 3-11, the next stage in NtCreateUserProcess is to find the appropriate Windows image that will run the executable file by the caller and to create a section object to later map it into the address space of the new process. If the call fails for any reason, it returns to CreateProcessInternalW with a failure state (look ahead to Table 3-8) that causes CreateProcessInternalW to attempt execution again.

![](bbox=[0.211, 0.622, 0.663, 0.883])

Figure 3-11 Choosing a Windows image to activate.