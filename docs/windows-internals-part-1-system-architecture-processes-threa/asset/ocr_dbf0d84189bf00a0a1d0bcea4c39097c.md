# Process Monitor - Sysinternals.www.sysinternals.com

File Edit Event Tools Options Help

| Process Name | Location | Path |
| --- | --- | --- |
| zcmd.exe | 14524 | CreateFile | C:\Users\pavei\*
| zcmd.exe | 14524 | QueryDirectory | C:\Users\pavei\*
| zcmd.exe | 14524 | QueryDirectory | C:\Program Files (x86)\Common Files\Microsoft Online Service\*
| zcmd.exe | 14524 | CreateFile | C:\Program Files (x86)\Common Files\Microsoft Online Service\*
| zcmd.exe | 14524 | CreateFile | C:\Windows\System32\*
| zcmd.exe | 14524 | CreateFile | C:\Windows\System32\*
| zcmd.exe | 14524 | CreateFile | C:\Windows\System32.COM
| zcmd.exe | 14524 | CreateFile | C:\Windows\System32.EXE
| zcmd.exe | 14524 | CreateFile | C:\Users\pavei\*
| zcmd.exe | 14524 | RegOpenKey | HKLM\SOFTWARE\WINDOWS\NT\CURRENTUSER\*
| zcmd.exe | 14524 | RegQueryKeyInformation | HKLM\SOFTWARE\Microsoft\Agent\Process\ivotepad.exe
| zcmd.exe | 14524 | RegSetValue | C:\WINDOWS\system32\notepad.exe
| zcmd.exe | 14524 | CreateProcess | 
| zcmd.exe | 14524 | TerminateProcess | 

Showing 3,428 of 233,905 events (1.4%) Back by virtual memory

As with this other event in Process Monitor's, you can see whether each part of the process-creation flow was performed in user mode or kernel mode, and by which routes, by looking at the stack of event. To do this, double-click the RegOpenKey event and switch to the Stack tab. The following screenshot shows the stack on a 64-bit Windows 10 machine:

# Event Properties

| Frame | Module | Location | Address | Path |
| --- | --- | --- | --- | --- |
| K 0 | ntdll.dll | | 0x77ff000084f08640 | C:\WINDOWS\system32\ntdll.dll
| K 1 | kernel32.dll | | 0x77ff000042f04238 | C:\WINDOWS\system32\kernel32.dll
| K 2 | ntdll.dll | OpenPaseKey = +0x17 | 0x77ff000031f0316 | C:\WINDOWS\system32\ntdll.dll
| K 3 | kernel32.dll | NtCreateKey = +0x1ec | 0x77ff000031f037c | C:\WINDOWS\system32\kernel32.dll
| K 4 | ntdll.dll | NtOpenKey = +0x2a6 | 0x77ff000031f03ae | C:\WINDOWS\system32\ntdll.dll
| K 5 | ntdll.dll | | 0x77ff000031f0394 | C:\WINDOWS\system32\ntdll.dll
| K 6 | ntdll.dll | ServiceControlQueryEnd = +0x13 | 0x77ff000031f0313 | C:\WINDOWS\system32\ntdll.dll
| K 7 | ntdll.dll | ServiceLink | 0x77ff000031f03560 | C:\WINDOWS\system32\ntdll.dll
| K 8 | ntdll.dll | RegSetValue = +0x41 | 0x77ff000031f034a6 | C:\WINDOWS\system32\ntdll.dll
| K 9 | ntdll.dll | NtCloseFile = +0x4e | 0x77ff000031f034b1 | C:\WINDOWS\system32\ntdll.dll
| K 10 | ntdll.dll | NtCreateFile = +0x1c | 0x77ff000031f033de | C:\WINDOWS\system32\ntdll.dll
| K 11 | ntdll.dll | ServiceControlQueryEnd = +0x13 | 0x77ff000031f0313 | C:\WINDOWS\system32\ntdll.dll
| U 12 | rtdll.dll | | 0x7ffa2522b2a4 | C:\WINDOWS\system32\rtdll.dll
| U 13 | kernel32.dll | CreateFile = +0x217 | 0x77ff000031f03c6 | C:\WINDOWS\system32\kernel32.dll
| U 14 | kernel32.dll | CreateProcess = +0x22 | 0x77ff000031f03e8 | C:\WINDOWS\system32\kernel32.dll
| U 15 | kernel32.dll | CreateProcessW = +0x53 | 0x77ff000031f03d5 | C:\WINDOWS\system32\kernel32.dll
| U 16 | ntdll.dll | | 0x77ff000031f035c | C:\WINDOWS\system32\ntdll.dll
| U 17 | ntdll.dll | | 0x77ff63b050b4b | C:\WINDOWS\system32\ntdll.dll
| U 18 | ntdll.dll | WorkItemThread = +0x36d | 0x77ff63b0f3d36d | C:\WINDOWS\system32\ntdll.dll
| U 19 | ntdll.dll | DispatchPath = +0x95 | 0x77ff63b0f3af45 | C:\WINDOWS\system32\ntdll.dll
| U 20 | ntdll.dll | CreateType = +0x2a1 | 0x77ff63b0f58191 | C:\WINDOWS\system32\ntdll.dll
| U 21 | ntdll.dll | | 0x77ff63b0f5b05c | C:\WINDOWS\system32\ntdll.dll
| U 22 | kernel32.dll | BaseThreadThread = +0x2d0 | 0x77fa23988102 | C:\WINDOWS\system32\kernel32.dll
| U 23 | rtdll.dll | UserThreadStart = +0x34 | 0x77fa2527c5b44 | C:\WINDOWS\system32\rtdll.dll

Event Process Stack Stack

| Frame | Module | Location | Address | Path |
| --- | --- | --- | --- | --- |
| K 0 | ntdll.dll | | 0x77ff000084f08640 | C:\WINDOWS\system32\ntdll.dll
| K 1 | kernel32.dll | | 0x77ff000042f04238 | C:\WINDOWS\system32\kernel32.dll
| K 2 | ntdll.dll | OpenPaseKey = +0x17 | 0x77ff000031f0316 | C:\WINDOWS\system32\ntdll.dll
| K 3 | kernel32.dll | NtCreateKey = +0x1ec | 0x77ff000031f037c | C:\WINDOWS\system32\kernel32.dll
| K 4 | ntdll.dll | NtOpenKey = +0x2a6 | 0x77ff000031f03ae | C:\WINDOWS\system32\ntdll.dll
| K 5 | ntdll.dll | | 0x77ff000031f0394 | C:\WINDOWS\system32\ntdll.dll
| K 6 | ntdll.dll | ServiceControlQueryEnd = +0x13 | 0x77ff000031f0313 | C:\WINDOWS\system32\ntdll.dll
| K 7 | ntdll.dll | ServiceLink | 0x77ff000031f03560 | C:\WINDOWS\system32\ntdll.dll
| K 8 | ntdll.dll | RegSetValue = +0x41 | 0x77ff000031f034a6 | C:\WINDOWS\system32\ntdll.dll
| K 9 | ntdll.dll | NtCloseFile = +0x4e | 0x77ff000031f034b1 | C:\WINDOWS\system32\ntdll.dll
| K 10 | ntdll.dll | NtCreateFile = +0x1c | 0x77ff000031f033de | C:\WINDOWS\system32\ntdll.dll
| K 11 | ntdll.dll | ServiceControlQueryEnd = +0x13 | 0x77ff000031f0313 | C:\WINDOWS\system32\ntdll.dll
| U 12 | rtdll.dll | | 0x7ffa2522b2a4 | C:\WINDOWS\system32\rtdll.dll
| U 13 | kernel32.dll | CreateFile = +0x217 | 0x77ff000031f03c6 | C:\WINDOWS\system32\kernel32.dll
| U 14 | kernel32.dll | CreateProcess = +0x22 | 0x77ff000031f03e8 | C:\WINDOWS\system32\kernel32.dll
| U 15 | kernel32.dll | CreateProcessW = +0x53 | 0x77ff000031f03d5 | C:\WINDOWS\system32\kernel32.dll
| U 16 | ntdll.dll | | 0x77ff000031f035c | C:\WINDOWS\system32\ntdll.dll
| U 17 | ntdll.dll | | 0x77ff63b050b4b | C:\WINDOWS\system32\ntdll.dll
| U 18 | ntdll.dll | WorkItemThread = +0x36d | 0x77ff63b0f3d36d | C:\WINDOWS\system32\ntdll.dll
| U 19 | ntdll.dll | DispatchPath = +0x95 | 0x77ff63b0f3af45 | C:\WINDOWS\system32\ntdll.dll
| U 20 | ntdll.dll | CreateType = +0x2a1 | 0x77ff63b0f58191 | C:\WINDOWS\system32\ntdll.dll
| U 21 | ntdll.dll | | 0x77ff63b0f5b05c | C:\WINDOWS\system32\ntdll.dll
| U 22 | kernel32.dll | BaseThreadThread = +0x2d0 | 0x77fa23988102 | C:\WINDOWS\system32\kernel32.dll
| U 23 | rtdll.dll | UserThreadStart = +0x34 | 0x77fa2527c5b44 | C:\WINDOWS\system32\rtdll.dll

CHAPTER 3 Processes and jobs 151