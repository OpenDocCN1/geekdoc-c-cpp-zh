![](bbox=[0.16, 0.09, 0.94, 0.71])

Figure 18-3

Run-time dynamic linking enables a program to defer linking of a DLL until it’s certain that the functions in a DLL are required. This allows you to write a program that can choose to load one or more of a number of DLLs based upon input to the program so that only those functions that are necessary are actually loaded into memory. In some circumstances, this can drastically reduce the amount of memory required to run a program.

A program implemented to use run-time dynamic linking calls the Windows API function LoadLibrary() to load the DLL when it’s required. The address of a function within the DLL can then be obtained using a function GetProcAddress(). When the program no longer has a need to use the