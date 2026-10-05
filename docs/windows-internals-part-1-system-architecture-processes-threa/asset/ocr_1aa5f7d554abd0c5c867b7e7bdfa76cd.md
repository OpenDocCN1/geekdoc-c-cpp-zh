# Stage 1: Converting and validating parameters and flags

Before opening the executable to run, CreateProcessInternal performs the following steps:

+   1. The priority class for the new process is specified as independent bits in the CreationFlags parameter to the CreateProcess functions. Thus, you can specify more than one priority class for a single CreateProcess* resolves the question of which priority class to assign to the process by choosing the lowest-priority class set.

There are six process priority classes defined, each value mapped to a number:

+   * Idle or Low, as Task Manager displays it (4)
* Below Normal (6)
* Normal (8)
* Above Normal (10)
* High (13)
* Real-time (24)

The priority class is used as the base priority for threads created in that process. This value does not directly affect the process itself—only the threads inside it. A description of process priority class and its effects on thread scheduling appears in Chapter 4.

+   2. If no priority class is specified for the new process, the priority class defaults to Normal. If a Real-time priority class is specified for the new process and the caller's doesn't have the Increasing Scheduling Priority privilege (SE_INC_BASE_PRIORITY_NAME), the High class is used instead. In other words, process creation does not fail just because the caller has insufficient privileges to create the process in the Real-time priority class; the new process won't have as high a priority as Real-time.

+   3. If the creation flags specify that the process will be debugged, Kernel32 initiates a connection to the native debugging code in Ntdll.dll via DbgConnectDebug and gets a handle to the debug object from the current thread's environment block (TEB).

+   4. Kernel32.dll sets the default hard error mode if the creation flags specified one.

+   5. The user-specified attribute list is converted from Windows subsystem format to normal format and internal attributes are added to it. The possible attributes that can be added to the attribute list are listed in Table 3-7, including their documented Windows API counterparts, if any.

> Note The attribute list passed to CreateProcess* permits access to the caller information beyond a simple status code, such as the TEB address of the initial thread or information on the image section. This is necessary for protected processes because the parent cannot query this information after the child is created.