# TABLE 7-12 High-level comparison of UWP and desktop apps

| UWP App | Desktop (Classic) App |
|--- |--- |
| Device Support | Runs on all Windows device families | Runs on PCs only |
| APIs | Can access WinRT, subset of COM, and subset of Win32 APIs | Can access COM, Win32, and subset of WinRT APIs |
| Identity | Strong identity (static and dynamic) | Raw EXEs and processes |
| Information | Declarative APX manifest | Opaque binaries |
| Installation | Self-contained APX package | Loose files or MSI |
| App Data | Isolated per-user/per-app storage (local and roaming) | Shared user profile |
| Lifecycle | Participates in app resource management and PLM | Process-level lifecycle |
| Instancing | Single instance only | Any number of instances |

![](bbox=[0.125, 0.365, 0.725, 0.563])

# FIGURE 7-17 The Windows platform landscape.

A few items in Figure 7-17 are elaborating on:

+   - UWP apps can produce normal executables, just like desktop apps. Whahost.exe (%SystemRoot%\System32\whahost.exe) is used to host HTML/JavaScript-based UWP apps, which produce a DLL, not an executable.
- The UI is implemented by the Windows Runtime APIs, which are based on an enhanced version of COM. Language projections are provided for C++ (through proprietary language extensions known as C+/CX), .NET languages, and JavaScript. These projections make it relatively easy to access WinRT types, methods, properties, and events from developers' familiar environments.
- Several bridging technologies are available, which can transform other types of applications into UWP. See the MSD documentation for more information on using these technologies.
- The Windows Runtime is layered on top of the Windows subsystems like the .NET Framework. It has no kernel components and is not part of a different subsystem because it still leverages the Win32 APIs that the system offers. However, some policies are implemented in the kernel, as well as the general support for AppContainers.

686 CHAPTER 7 Security