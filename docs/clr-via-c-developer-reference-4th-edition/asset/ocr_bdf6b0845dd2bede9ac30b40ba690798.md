Furthermore, because the /out:Program.exe and the /t:exe command-line switches also match the C# compiler would choose as defaults, the following command line gives the same results too.

csc.exe Program.cs

If, for some reason, you really don't want the C# compiler to reference the MSCor.dll assembly, you can use the /nostlib switch. Microsoft uses this when building the MSCor.dll assembly itself. For example, the following command line will generate an error when CSC.exe attempts to compile the Program.cs file because the System.Console type is defined in MSCorLib.dll.

csc.exe /out:Program.exe /t:nostdlib Program.cs

Now, let's take a closer look at the Program.exe file produced by the C# compiler. What exactly is this file? For starters, it is a standalone executable (PE) file. This means that a machine running 32-bit or 64-bit versions of Windows would be able to load this and do something with. Windows supports three types of applications. To build a console user interface (CUI) application, specify the /t:exe switch; to build a graphical user interface (GUI) application, specify the /t:winex switch; and to build a Windows Store app, specify the /t:apparenterexe switch.

# Response Files

Before leaving the discussion about compiler switches, I'd like to spend a moment talking about response files. When you execute CSC.exe, the compiler opens response files and uses any switches that are specified in them though those were passed to CSC.exe on the command line. You instruct the compiler to use a response file by specifying its name on the command line preceded by an @ sign. For example, you could have a response file called MyProject.rsp that contains the following text.

```
/out:MyProject.exe
target:winex
```

To cause CSC.exe to use these settings, you invoke it as follows.

```
csc.exe @MyProject.rsp CodeFile1.cs CodeFile2.cs
```

This tells the C# compiler what to name the output file and what kind of target to create. As you can, response files are very convenient because you don't have to manually express the desired command-line arguments each time you want to compile your project.

The C# compiler supports multiple response files. In addition to the files you explicitly specify on the command line, the compiler automatically looks for files called CSC.rsp. When you run CSC.exe, it looks in the directory containing the CSC.exe for a global CSC.rsp file. Settings that you want applied to all of your projects should go in this file. The compiler aggregates and uses the settings in all of these response files. If you conflicting settings in the local and global response files, the settings in the local file override the settings in the global file. Likewise, any settings explicitly passed on the command line override the settings taken from a local response file.