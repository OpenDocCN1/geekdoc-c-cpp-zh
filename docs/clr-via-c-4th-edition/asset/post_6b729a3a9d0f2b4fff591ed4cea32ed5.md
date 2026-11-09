
## Loading the Common Language Runtime

Each assembly you build can be either an executable application or a DLL containing a set of types for use by an executable application. Of course, the CLR is responsible for managing the execution of code contained within these assemblies. This means that the .NET Framework must be installed on the host machine. Microsoft has created a redistribution package that you can freely ship to install the .NET Framework on your customers' machines. Some versions of Windows ship with the .NET Framework already installed.

You can tell if the .NET Framework has been installed by looking for the MSCorEE.dll file in the %SystemRoot%\System32 directory. The existence of this file tells you that the .NET Framework is installed. However, several versions of the .NET Framework can be installed on a single machine simultaneously. If you want to determine exactly which versions of the .NET Framework are installed, examine the subdirectories under the following directories:

```
%SystemRoot%\Microsoft.NET\Framework
%SystemRoot%\Microsoft.NET\Framework64
```

The .NET Framework SDK includes a command-line utility called CLRVer.exe that shows all of the CLR versions installed on a machine. This utility can also show which version of the CLR is being used by processes currently running on the machine by using the -all switch or passing the ID of the process you are interested in.

Before we start looking at how the CLR loads, we need to spend a moment discussing 32-bit and 64-bit versions of Windows. If your assembly files contain only type-safe managed code, you are writing code that should work on both 32-bit and 64-bit versions of Windows. No source code changes are required for your code to run on either version of Windows. In fact, the resulting EXE/DLL file produced by the compiler should work correctly when running on x86 and x64 versions of Windows. In addition, Windows Store applications or class libraries will run on Windows RT machines (which use an ARM CPU). In other words, the one file will run on any machine that has the corresponding version of the .NET Framework installed on it.

On extremely rare occasions, developers want to write code that works only on a specific version of Windows. Developers might do this when using unsafe code or when interoperating with unmanaged code that is targeted to a specific CPU architecture. To aid these developers, the C# compiler offers a /platform command-line switch. This switch allows you to specify whether the resulting assembly can run on x86 machines running 32-bit Windows versions only, x64 machines running 64-bit Windows only, or ARM machines running 32-bit Windows RT only. If you don't specify a platform, the default is anycpu, which indicates that the resulting assembly can run on any version of Windows. Users of Visual Studio can set a project's target platform by displaying the project's property pages, clicking the Build tab, and then selecting an option in the Platform Target list (see Figure 1-3).

In Figure 1-3, you'll notice the Prefer 32-Bit check box. This check box is only enabled when Platform Target is set to Any CPU and if the project type produces an executable. If you select the Prefer 32-Bit check box, then Visual Studio spawns the C# compiler specifying the /platform:anycpu32bitpreferred compiler switch. This option indicates that the executable should run as a 32-bit

**TABLE 1-2** Effects of /platform on Resulting Module and at Run Time

| /platform Switch | Resulting Managed Module | x86 Windows | x64 Windows | ARM Windows RT |
|---|---|---|---|---|
| anycpu (the default) | PE32/agnostic | Runs as a 32-bit application | Runs as a 64-bit application | Runs as a 32-bit application |
| anycpu32bitpreferred | PE32/agnostic | Runs as a 32-bit application | Runs as a 32-bit application | Runs as a 32-bit application |
| x86 | PE32/x86 | Runs as a 32-bit application | Runs as a WoW64 application | Doesn't run |
| x64 | PE32+/x64 | Doesn't run | Runs as a 64-bit application | Doesn't run |
| ARM | PE32/ARM | Doesn't run | Doesn't run | Runs as a 32-bit application |

After Windows has examined the EXE file's header to determine whether to create a 32-bit or 64-bit process, Windows loads the x86, x64, or ARM version of MSCorEE.dll into the process's address space. On an x86 or ARM version of Windows, the 32-bit version of MSCorEE.dll can be found in the %SystemRoot%\System32 directory. On an x64 version of Windows, the x86 version of MSCorEE.dll can be found in the %SystemRoot%\SysWOW64 directory, whereas the 64-bit version can be found in the %SystemRoot%\System32 directory (for backward compatibility reasons). Then, the process's primary thread calls a method defined inside MSCorEE.dll. This method initializes the CLR, loads the EXE assembly, and then calls its entry point method (Main). At this point, the managed application is up and running.[1]

> **Note** Assemblies built by using version 1.0 or 1.1 of Microsoft's C# compiler contain a PE32 header and are CPU-architecture agnostic. However, at load time, the CLR considers these assemblies to be x86 only. For executable files, this improves the likelihood of the application actually working on a 64-bit system because the executable file will load in WoW64, giving the process an environment very similar to what it would have on a 32-bit x86 version of Windows.

If an unmanaged application calls the Win32 LoadLibrary function to load a managed assembly, Windows knows to load and initialize the CLR (if not already loaded) in order to process the code contained within the assembly. Of course, in this scenario, the process is already up and running, and this may limit the usability of the assembly. For example, a managed assembly compiled with the /platform:x86 switch will not be able to load into a 64-bit process at all, whereas an executable file compiled with this same switch would have loaded in WoW64 on a computer running a 64-bit version of Windows.

> [1] Your code can query Environment's Is64BitOperatingSystem property to determine if it is running on a 64-bit version of Windows. Your code can also query Environment's Is64BitProcess property to determine if it is running in a 64-bit address space.

## Executing Your Assembly's Code

As mentioned earlier, managed assemblies contain both metadata and IL. IL is a CPU-independent machine language created by Microsoft after consultation with several external commercial and academic language/compiler writers. IL is a much higher-level language than most CPU machine languages. IL can access and manipulate object types and has instructions to create and initialize objects, call virtual methods on objects, and manipulate array elements directly. It even has instructions to throw and catch exceptions for error handling. You can think of IL as an object-oriented machine language.

Usually, developers will program in a high-level language, such as C#, Visual Basic, or F#. The compilers for these high-level languages produce IL. However, as any other machine language, IL can be written in assembly language, and Microsoft does provide an IL Assembler, ILAsm.exe. Microsoft also provides an IL Disassembler, ILDasm.exe.

Keep in mind that any high-level language will most likely expose only a subset of the facilities offered by the CLR. However, the IL assembly language allows a developer to access all of the CLR's facilities. So, should your programming language of choice hide a facility the CLR offers that you really want to take advantage of, you can choose to write that portion of your code in IL assembly or perhaps another programming language that exposes the CLR feature you seek.

The only way for you to know what facilities the CLR offers is to read documentation specific to the CLR itself. In this book, I try to concentrate on CLR features and how they are exposed or not exposed by the C# language. I suspect that most other books and articles will present the CLR via a language perspective, and that most developers will come to believe that the CLR offers only what the developer's chosen language exposes. As long as your language allows you to accomplish what you're trying to get done, this blurred perspective isn't a bad thing.

![](img/857bdf6cef9e242b53a37f88df9a1287_36_0.png)

> **Important** I think this ability to switch programming languages easily with rich integration between languages is an awesome feature of the CLR. Unfortunately, I also believe that developers will often overlook this feature. Programming languages such as C# and Visual Basic are excellent languages for performing I/O operations. APL is a great language for performing advanced engineering or financial calculations. Through the CLR, you can write the I/O portions of your application in C# and then write the engineering calculations part in APL. The CLR offers a level of integration between these languages that is unprecedented and really makes mixed-language programming worthy of consideration for many development projects.

To execute a method, its IL must first be converted to native CPU instructions. This is the job of the CLR's JIT (just-in-time) compiler.

Figure 1-4 shows what happens the first time a method is called.

Just before the Main method executes, the CLR detects all of the types that are referenced by Main's code. This causes the CLR to allocate an internal data structure that is used to manage access
