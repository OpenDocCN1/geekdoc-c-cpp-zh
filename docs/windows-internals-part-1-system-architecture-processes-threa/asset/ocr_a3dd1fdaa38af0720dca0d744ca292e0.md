This stack shows that you already reached the part of process creation performed in kernel mode (through NtCreateUserProcess) and that the helper PspAllocateProcess is responsible for this check.

Going down the list of events after the thread and process have been created, you will notice three groups of events:

+   - A simple check for application-compatibility flags, which will let the user-mode process-creation code know if checks the application-compatibility database are required through the shim engine.

+   - Multiple reads to SxS (search for By-Side-Side), Manifest, and MUI/Language keys, which are part of the assembly framework mentioned earlier.

+   - File I/O to one or more .db files, which are the application-compatibility databases on the system. This I/O is where additional checks are done to see if the shim engine needs to be invoked for this. Because Notepad is a well-behaved Microsoft program, it doesn't require any shims.

The following screenshot shows the next series of events, which happen inside the Notepad process itself. These are actions initiated by the user-mode thread wrapper in kernel mode, which performs the actions described above. The first two are Notepad.exe and Ntdll.dll image debug notification messages, which can be generated only when code is running inside Notepad's process context and for the context of the process.

![](bbox=[0.146, 0.523, 0.853, 0.765])