2. The address on the Ldr line is a pointer to the PEB_LDR_DATA structure described earlier. Notice that WinD shows you the address of the three lists, and dumps the initialization order list for you, displaying the full path, time, and base address of each module.

3. You can analyze each module entry on its own by going through the module list and dumping the data at each address, formatted as a LDR_DATA_TABLE_ENTRY structure. Instead of doing this for each entry, however, WinD can do some of the work by the !list extension and the following syntax:

```
!list -x "dt ntdll_LDR_DATA_TABLE_ENTRY" @C++(&$peb)->Ldr->InLoadOrderModuleList
+0x00 InLoadOrderLinks : :LIST_ENTRY [ 00000028'15d23d10 000007fe'85d23b0 ]
+0x10 MemoryOrderLinks : :LIST_ENTRY [ 00000028'15d23d20 000007fe'85d23c0 ]
+0x20 InitializationOrderLinks : :LIST_ENTRY [ 00000000'00000000 ]
+0x30 Base : 000007ff7f20b6000 Void
+0x38 EntryPoint : 000007ff7f028b7d0 Void
+0x40 SizeOfImage : 0x410000
+0x48 FullDllName : :UNICODE_STRING "C:\Windows\System32\notepad.exe"
+0x58 BaseName : :UNICODE_STRING "notepad.exe"
+0x68 FlagGroup : [4] "???"
+0x68 Flags : 0xa2cc
```

4. You should see the entries for each module:

Although this section covers the user-mode loader in Ntdll.dll, note that the kernel employs its own loader for drivers and dependent DLLs, with a similar loader structure called KLDR_DATA_TABLE_ENTRY inside. Likewise, the kernel-mode loader has its own database of entries, which is directly accessible through the PsActiveModuleList global variable. You can use a !list command as shown in the preceding experiment by replacing the pointer at the end of the command with !PsActiveModuleList and using the new structure/module: !list!KLDR_DATA_TABLE_ENTRY !PsActiveModuleList.

Looking at the list in this format gives you some extra insight into the loader, such as the Flags field, which contains state information that !peb on its own would not show you. See Table 3-10 for their meaning. Because both the kernel and user-mode loaders use this structure, the meaning of the flags is not always the same (some of which may exist in the kernel structure as well).