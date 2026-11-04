# IMAGE FILE EXECUTION OPTIONS

In fact, the problem of debugging a startup path has been around since the early days of Windows. It's not really a problem, though. The designers of the loader that is used to run executables on Windows envisioned this problem (or likely hit the difficulty themselves plenty of times).

To make such debugger scenarios more appealing, they put in a grand hack called Image File Execution Options, which is a Registry-based setting that can be specified on a per-program basis. You can find it under the Local Machine hive of the Registry at HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options. Each executable whose process creation should be subject to tweaks applied by the loader has a subkey that specifies such options. For example, settings affecting process creation for notepad.exe executable images live under a subkey called notepad.exe.

The Debugger setting enables you to cause the loader to start a specified program rather than the original executable. The original executable's path is passed to the "debugger" executable as the first command-line argument. This way, a debugger can be configured to intercept any creation of a process for a given executable.

An example of the use of Break is shown here:

```
static void Main()
{
    Debugger.Break();
    // More code goes here...
}
```

The code's behavior depends on the presence of an attached debugger. If that's the case, our call to Break simply causes us to break into the debugger at the line of the call. If no debugger is attached yet, a dialog displays, as shown in Figure 27.6.

![](bbox=[0.1, 0.8, 0.48, 0.95])

FIGURE 27.6 Result of a call to Debugger.Break without a debugger attached.

Depending on the machine's configuration (that is, whether a debugger has been set up), the dialog's look will vary. In any case, you can now attach a debugger to the process that has triggered a Break call, and doing so puts you straight on the line where the