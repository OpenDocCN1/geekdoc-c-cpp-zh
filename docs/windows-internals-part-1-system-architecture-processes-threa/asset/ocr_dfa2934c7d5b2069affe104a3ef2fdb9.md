+   Loading and unloading DLLs at run time, as well as on demand, and maintaining a list of all loaded modules (the module database).

+   Handling manifest files, needed for Windows Side-by-Side (SxS) support, as well as Multiple Language User Interface (MUI) files and resources.

+   Reading the application compatibility database for any shims, and loading the shim engine DLL if required.

+   Enabling support for API Sets and API redirection, a core part of the One Core functionality that allows creating Universal Windows Platform (UWP) applications.

+   Enabling dynamic runtime compatibility mitigations through the SwitchBack mechanism as well as interfacing with the shim and and Verifier mechanisms.

As you can see, most of these tasks are critical to enabling an application to actually run. Without them, everything from calling external functions to using the heap would immediately fail. After the process has been created, the loader calls the NtContinue native API to continue execution on an exception frame located on the stack, as an exception handler would. This exception frame, built by the kernel as we saw in an earlier section, contains the entry point of the application. Therefore, because the loader doesn't use a standard call or jump into the running application, you will never see the loader initialization functions as part of the call tree in a stack trace for a thread.

# EXPERIMENT: Watching the image loader

In this experiment, we use global flags to enable a debugging feature called loader snaps. This allows you to debug output from the loader using debugging application startup.

+   1. From the directory where you've installed WinDbg, launch the Gflags application, and then click the Image File tab.

+   2. In the Image field, press Notepad.exe, and press the Tab key. This should enable the various options. Select the Loader Snaps option and then click OK or Apply.

+   3. Now launch WinDbg, select the File menu, choose Open Executable, and navigate to c:\windows\system32\notepad.exe to launch it. You should see a couple of screens of debug information shown here:

```
06F90:020 02405218 - LdrInitializeProcess INFO: Beginning execution of
otepad.exe (C:\Windows\notepad.exe)
Current directory: C:\Program Files (x86)\Windows Kits\10\Debuggers\nPackage directories: (null)
06F90:020 02405218 - LdrLoadDll1 ENTER: DLL name: KERNEL332.DLL
06F90:020 02405218 - LdrLoadDll1Internal ENTER: DLL name: KERNEL.32.DLL
06F90:020 02405218 - LdrFindKnownDll1 ENTER: DLL name: KERNEL.32.DLL
06F90:020 02405218 - LdrFindKnownDll1 RETURN: Status: 0x00000000
```