13. It reads the NumberOfSessions value from the HKLM\SYSTEM\CurrentSet\Control\Session Manager key, but ignores it if the system is in manufacturing mode.

14. It reads the file rename operations listed under the PendingFileRenameOperations and PendingFileRenameOperations2 from the HKLM\SYSTEM\CurrentSet\Control\Session Manager key.

15. It reads the value of the AllowProtectedRenames, ClearTempFiles, TempDirectory, and DisableWpbtExecution values in the HKLM\SYSTEM\CurrentSet\Control\Session Manager key.

16. It reads the list of DLLs in the ExcludeFromKnownList value found in the HKLM\SYSTEM\CurrentSet\Control\Session Manager key.

17. It reads the paging file information stored in the HKLM\SYSTEM\CurrentSet\Control\Session Manager\Memory Management key, such as the PagingFiles and ExistingPage list values and the Pagefile0Volume and WaitForPagingFiles configuration values.

18. It reads and saves the values stored in the HKLM\SYSTEM\CurrentSet\Control\Session Manager\DOS Devices key.

19. It saves the KnownDlls value stored in the HKLM\SYSTEM\CurrentSet\Control\Session Manager key.

20. It creates system-wide environment variables as defined in HKLM\SYSTEM\CurrentSet\Control\Session Manager\Environment.

21. It creates the \KnownDlls directory, as well as \KnownDlls2 on 64-bit systems with WoW64.

22. It creates symbolic links for devices defined in HKLM\SYSTEM\CurrentSet\Control\Session Manager\DOS Devices under the \Global?\ directory in the object manager namespace.

23. It creates a root \Sessions directory in the object manager namespace.

24. It creates protected mailslot and name prefixes to prevent service attacks from spoofing-attacks that could occur if a malicious user-mode application executes before a service.

25. It runs the programs from BootExecute and BootExecuteNoPnP list parsed earlier. The default is Autochk.exe, which performs a disk check.

26. It initializes the rest of the registry (HKLM software, SAM, and security hives).

27. Unless disabled by the registry, it executes the Windows Platform Base Binary (WPBT) binary registered in registry ACPI table. This is used by anti-theft vendors to force the execution of a very early Windows binary that can call home or set up other services for execution, even on a freshly installed system. These processes must link with Ntdll.dll (only that is, belong to the native subsystem).

28. It processes pending file names as specified in the registry keys earlier unless this is a Windows Recovery Environment boot.