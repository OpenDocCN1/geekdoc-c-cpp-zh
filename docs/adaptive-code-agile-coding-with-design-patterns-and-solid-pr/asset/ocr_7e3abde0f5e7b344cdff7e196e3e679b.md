+   - If the assembly could not be found in the GAC, the CLR starts probing a variety of directories in search of it. The directories searched depend on the app.config settings. If there is a code-base element in the app.config, that location is checked—and if the assembly is not found—no other locations are subsequently checked. However, the default is for the application’s root directory to be searched, which is typically the /bin folder that relates to the entry point or web application. If the assembly cannot be found there, the resolution process fails and an exception is thrown by the CLR. Typically, this results in the termination of the application.

![](bbox=[0.156, 0.208, 0.838, 0.68])

**FIGURE 3-12** A brief overview of the assembly resolution process.

**The Fusion log**  This is a very useful tool for debugging failed attempts by the CLR to bind to an assembly at run time. Rather than trying to step through the application in the Visual Studio debugger, it is better to turn Fusion on and read the log file that results.

To enable Fusion you must edit the Windows registry, as shown in the following code.

```
HKLM\Software\Microsoft\Fusion\ForceLog 1
HKLM\Software\Microsoft\Fusion\LogPath C:\FusionLogs
```