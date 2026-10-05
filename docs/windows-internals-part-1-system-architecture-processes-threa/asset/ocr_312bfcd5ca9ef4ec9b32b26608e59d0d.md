Now that a table of valid functions exists, all that simple function would need to do is compare the target of the CALL or JMP instruction with one of the functions in the table. Algorithmically, this would result in an O(n) algorithm, where the number of functions needed to check would be equivalent, in the worst case, to the number of functions in the table. Clearly, linearly scanning an array over every single indirect change in control flow would bring a program to knees, so operating system support is needed to perform CFG checks efficiently. We'll see in the next section how Windows can achieve this.

# EXPERIMENT: Control Flow guard information

The DumpBin Visual Studio tool can show some basic CFG information. The following dumps and header configuration for smss:

```
c> dumpbin /headers /loadconfig:c:\windows\system32\smss.exe
Microsoft (R) COFF/PE Dumper Version 14.00.24215.1
Copyright (C) Microsoft Corporation. All rights reserved.
Dump of file c:\windows\system32\smss.exe
PE signature
File Type: EXECUTABLE IMAGE
FILE HEADER VALUES
8664 machine (x64)
6 number of sections
5789A7D file time stamp Sat Jul 16 05:22:53
0 file pointer to symbol table
0 number of symbols
F0 size of optional header
22 characteristics
Executable
Application can handle large (>2GB) addresses
```

```
OPTIONAL HEADER VALUES
20B magic # (PE32)
14.00 linker version
12800 size of code
EC00 size of initialized data
0 size of uninitialized data
1080 entry point (0000001400001080) NtProcessStartup
1000 base of code
14000000 image base (0000001400000000 to 0000001400024FF)\)
1000 section alignment
200 file alignment
10.00 operating system version
10.00 image version
10.00 subsystem version
0 Win32 version
25000 size of image
400 size of headers
270FD checksum
1 subsystem (Native)
4160 DLL characteristics
```