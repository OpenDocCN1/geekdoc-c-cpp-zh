Now, let's explain the dll itself. Just like the application (exe) the dynamic link library must have its own entry point. Its prototype must match the following signature:

```
BOOL WINAPI DllMain(HINST hInstance, DWORD dwReason, LPVOID
lpReserved);
```

When the dll is loaded, its execution starts from this method. You could distinguish reasons why this method was loaded. These can be as follows:

+   - The DLL_PROCESS_ATTACH method notifying that the application just loaded the dll
- The DLL_PROCESS_DETACH method notifying that the application just unloaded the dll
- The DLL_THREAD_ATTACH method notifying that the application where the dll is loaded created a new thread
- The DLL_THREAD_DETACH method notifying that the thread is exiting and some cleanup can be done

We do all our inside DLL_PROCESS_ATTACH. Inside our main application, we create a file mapping necessary for communication between the application and the dll, which we'll explain later. Inside the dll, we first open the file mapping, using the OpenFileMapping API. If the mapping is opened, we write the handle to the hLibrary attribute. We need this handle later to unload the library from the target process, when we finish our work. Next, we call the ChangWindowTitle method. This function tries to find the main window handle using FindMainWindow. If a handle is found, we can alter the window title.

The FindWindow method uses the EnumWindows API to enumerate all top-level windows. User must provide a pointer to a user-defined function (called callback) as the argument passed to EnumWindows. This callback is called by the operating system for each window handle that belongs to the OS. We can use this feature to query window handle for owning the thread (process). We can achieve this using the GetWindowThreadProcessId.

If we find a window that belongs to the target process, we should also check if that is the main window. For task, we use the IsMainWnd method. This method calls GetWindow with GW_OWNER as the second parameter and if the value returned is 0 (zero), it will query the window visibility using the IsVisible API, making sure that, if visible, it is the main application window from the target process. ChangeWindowTitle returns, we open an event that we use for notifying our application that the job done and we can unload the library. We set the event to the signaled state using the SetEvent API.