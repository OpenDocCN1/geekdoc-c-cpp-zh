# The Concepts of Process and Thread

```
FreeLibrary(hDll);
else {
    cout << "Cannot load ntdll.dll!" << endl
    cout << "Error code:\t" << GetLastError() << endl;
}
else {
    cout << "Cannot start process!" << endl;
    cout << "Error code:\t" << GetLastError() << endl;
}
return 0;
```

# How it works...

For this example, we used some additional header files: Winternal.h and Windows.h. Header Winter include includes for the majority of Windows' internal routines and data representation; this includes the PROCESS_BASIC_INFORMATION structure with the following:

```
typedef struct PROCESS_BASIC_INFORMATION {
    VOID Reserved1;
    PEB BaseAddress;
    VOID Reserved2[2];
    ULONG_PTR UniqueProcessId;
    VOID Reserved3;
} PROCESS_INFORMATION;
```

The preceding structure is used by the operating system in calls made between the user mode and kernel mode subroutines. In combination with the PROCESSINFORMATIONCLASS::ProcessBaseInformation, we use the UniqueProcessId attribute to obtain the process identifier, only as a demonstration.

First, we define QUERYINFORMATION, a typedef for the NtQueryInformationFunction loaded from the ntdll.dll library. When the address of the function is obtained using the GetProcAddress Win32 API, we can query for the PROCESS_BASIC_INFORMATION object. Pay attention to the PebBaseAddress field; it is a pointer to the PCB of the newly created process. If you want to check the newly created process, you will have to use the ReadProcessMemory routine in runtime, because the memory to which PebBaseAddress points belongs to the newly created process.

+   54