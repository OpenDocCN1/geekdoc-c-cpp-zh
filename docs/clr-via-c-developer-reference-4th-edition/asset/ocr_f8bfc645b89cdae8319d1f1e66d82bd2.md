# Loading the Common Language Runtime

Each assembly you build can be either an executable application or a DLL containing a set of types for use by an executable application. Of course, the CLR is responsible for managing the execution of code contained within these assemblies. This means that the .NET Framework must be installed on the host machine. Microsoft has created a distribution package that you can freely ship to install the .NET Framework on your customers' machines. Some versions of Windows ship with .NET Framework already installed.

You can tell if the .NET Framework has been installed by looking for the MSCore.dll file in the %SystemRoot%System32 directory. The existence of this file tells you that the .NET Framework is installed. however, several versions of the .NET Framework can be installed on a single machine simultaneously. If you want to determine which versions of the .NET Framework are installed, examine the subdirectories under the following directories:

```
%SystemRoot%\Microsoft\.Framework
%SystemRoot%\Microsoft\.Framework\64
```

The .NET Framework SDK contains a command-line utility called CLRx.exe that shows all of the CLR versions installed on a machine. This utility can also show which version of the CLR is being used by processes currently running on the machine using the -all switch or passing the ID of the process you are interested in.

Before we start looking at how the CLR loads, we need to spend a moment considering 32-bit and 64-bit versions of Windows. If your assembly files contain only type-safe managed code, you are writing code that should run on both32-bit and 64-bit versions of Windows. Source code changes are required for your code to run on either version of Windows. The resulting EXE/DLL fact produced by the compiler should work when running on x86 and x64 versions of Windows. In addition, Windows Store applications or class libraries will run on Windows RT machines (which use an ARM CPU). In other words, the one file will run on any machine that has the corresponding version of the .NET Framework installed on it.

On extremely rare occasions

In Figure 1-3, you'll notice the Prefer 32-bit check box. This box is only enabled when Platform is set to Any CPU and the project type produces an executable. If you select the Prefer 32-bit check box, then Visual Studio shows the C# compiler specifying the /platform:preferred switch. This option indicates that the executable should run as a 32-bit