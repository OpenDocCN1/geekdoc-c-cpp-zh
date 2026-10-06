
# Using remote threading

So far, we were focusing on situations where we had total control of all application parts and the execution itself. In practice, this is far from the truth. In many situations, you would have to continue where some other developer stopped or you would have to use completed parts or external applications where changing the code is not possible. Even in such a situation, sometimes there is a need to change application behavior, which we will explain later.

When we are unable to change the code, we could use remote threading. Remote threading is a feature presented by the Windows operating system, starting from XP OS, and maintained in all newer versions. A remote thread is a thread like any other, with the difference being that the remote thread does not execute under the process context but in the address space of the remote process. It is an excellent feature with the earlier described scenarios.

There are few ways in which you can start a remote thread: using the CreateRemoteThread API, the SetWindowHook API, or the undocumented NtCreateThread API.

We'll focus on the CreateRemoteThread API. In our example, we will assume that Windows calculator is some external application we can't change, and yet we have to alter its main window title (for some reason). Even though we could change the title of the calculator window from our application without using a remote thread, we chose this scenario for the simplicity of example.

# Getting ready

Make sure Visual Studio is up and running.

# How to do it...

Now, let's create our program and explain its structure. Perform the following steps:

- Create a new empty C++ application named RemoteThreading.
- Open Windows Explorer and navigate to your solution folder. Create a new text file named common.txt. Change its extension to .h.
- Open Solution Explorer and right-click on the RemoteThreading solution. Select the Adding Item option and add common.h. Open common.h. Copy and paste the following code:

```cpp
#include <windows.h>
#include <tchar.h>

#define MAPPING_NAME T("__comm_61524_map__")
```

```cpp
#define EVENT_NAME    _T("__evnt_68435_rst__")

typedef struct {
    HMODULE hLibrary;
} COMM_OBJECT, *PCOMM_OBJECT;
```

- 4. Open Solution Explorer and under the project RemoteThreading right-click on Source files. Add a new source file named main.cpp.

- 5. Add the following code:

```cpp
#include <windows.h>
#include <char.h>
#include "..\common.h"

int __stdcall RemoteLoadLibrary(HANDLE hProcess
```

![](img/412b0f5bbb36adcce2ddd2d5b7416516_386_0.png)

```cpp
BOOL bSuccess = WriteProcessMemory(hProcess, lpRemoteMem,
szLibraryName, uMemSize, NULL);
if (bSuccess == STATUS_ACCESS_VIOLATION || bSuccess == FALSE)
{
    _printf_s(
        T("Could not write virtual memory!\nError:%t\n"),
        GetLastError());
    VirtualFreeEx(hProcess, lpRemoteMem, 0, MEM_RELEASE);
    return -1;
}

HANDLE thread = CreateRemoteThread(hProcess, NULL, 0, 
lLoadLibrary, lpRemoteMem, 0, NULL);
if (hThread == NULL)
{
    _printf_s(
        T("Could not create thread!\nError:%t\n"),
        GetLastError());
    VirtualFreeEx(hProcess, lpRemoteMem, 0, MEM_RELEASE);
    return -1;
}

WaitForSingleObject(hThread, INFINITE);
VirtualFreeEx(hProcess, lpRemoteMem, 0, MEM_RELEASE);
CloseHandle(hThread);

return 0;
```

```cpp
int _stdcall RemoteFreeLibrary(HANDLE hProcess, HMODULE hLib)
{
    LPTHREAD_START_ROUTINE lpLoadLibrary = (LPTHREAD_START_ROUTINE)GetProcAddress(GetModuleHandleA("Kernel32.dll"), "FreeLibrary");
    if (lpLoadLibrary == NULL)
    {
        return -1;
    }
    if (hProcess)
    {
        _printf_s(_T("Handle to Process 0xx was NULL!\n"), (int)hProcess);
        return -1;
    }

HANDLE hThread = CreateRemoteThread(hProcess, NULL, 0, 
lLoadLibrary, hLib, 0, NULL);
```

```cpp
if (hThread == NULL)
{
    _printf_s(
        _T("Could not create remote thread!\nError:%t\n"),
        GetLastError());
    return -1;
}

WaitSingleObject(hThread, INFINITE);

CloseHandle(hThread);

return 0;
```

```cpp
int main(void)
{
    char* szLibrary = PHYSICAL_PATH_TO_YOUR_DLL;

    HANDLE hMapping = CreateFileMapping((HANDLE)-1, NULL,
        PAGE_READWRITE, 0, 0, sizeof(COMM_OBJECT), MAPPING_NAME);
    HANDLE hEvent = CreateEvent(NULL, TRUE, NULL, EVENT_NAME);

    STARTUPINFO si = { sizeof(si) };
    PROCESS_INFORMATION pi = { 0 };

    if (!CreateProcess(NULL, szLibrary, NULL, NULL, FALSE, 0, NULL, NULL, &si, &pi))
    {
        _printf_s(_T("Failed to create process!\nError:%t\n"), GetLastError());
        return 1;
    }

    LPVOID lpRemoteMem = VirtualAllocEx(pi.hProcess, NULL, strlen(szLibrary) + 1, MEM_COMMIT | PAGE_READWRITE);
    WriteProcessMemory(pi.hProcess, lpRemoteMem, szLibrary, strlen(szLibrary) + 1, NULL);

    HANDLE hThread = CreateRemoteThread(pi.hProcess, NULL, 0,
        (LPTHREAD_START_ROUTINE)GetProcAddress(GetModuleHandleA("Kernel32.dll"), "LoadLibrary"),
        lpRemoteMem, 0, NULL);

    if (hThread == NULL)
    {
        _printf_s(_T("Could not create remote thread!\nError:%t\n"), GetLastError());
    }
    else
    {
        WaitForSingleObject(hThread, INFINITE);
        VirtualFreeEx(pi.hProcess, lpRemoteMem, 0, MEM_RELEASE);
        CloseHandle(hThread);
    }

    CloseHandle(pi.hProcess);
    CloseHandle(pi.hThread);

    return 0;
}
```

# How it works..

First, we have created common.h, in order to define the structure, event, and mapping name that both projects will use. We must divide our program into two parts: exe and dll. We must create exe to run in an application. We must create a separate dll because the remote thread address will reside in that. In our previous examples, all thread addresses were in the same process itself, because the thread was executing in the address space of the current process.
