# Thread Synchronization and Concurrent Operations

```
ofn.hwndOwner = hWnd;
ofn.lpstrFile = szFile;
ofn.lpstrFile[] = '\00';
ofn.nMaxFile = sizeof(szFile);
ofn.lpstrFilter = "All Files\0*.*\0TXT\*\00";
ofn.nFilterIndex = 1;
ofn.lpstrFileTitle = NULL;
ofn.nMaxFile = 0;
ofn.lpstrInitialDir = NULL;
ofn.Flags = OFN_MUSTEXIST;
if (GetOpenFileNameA(&ofn) == TRUE)
{
    strncpy(szFile, MAX_PATH - 1, szFile);
    return TRUE;
}
return FALSE;
```

# How it works...

This is a slightly different approach than the one used in our previous example. Instead of creating as many threads as there are processors, we instantiate a semaphore object where the initial as the maximum count of parallel operations will not exceed the number of CPUs. It is similar; the only difference is the technique used and approach selected. We have asked the system for the semaphore object inside the StartAddress routine. After successful operation, we are releasing the semaphore by decrementing it by:

```
WaitForSingleObject( hSemaphore, INFINITE );
ReleaseSemaphore( hSemaphore, 1, NULL );
```

# There's more...

Again, the most important part was to properly select the synchronization spots as well as proper synchronization object selection. We've intentionally selected semaphore in order to demonstrate to the user that the first solution isnt always the only solution. Fortunately, Windows provides a variety of synchronization objects, and developers should be aware of each one of them in order to select the most appropriate one in their development.

![](bbox=[0.181, 0.837, 0.222, 0.856])