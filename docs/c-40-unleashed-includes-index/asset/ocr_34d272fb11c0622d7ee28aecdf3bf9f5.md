and so did Java with its virtual machine (JVM). What distinguishes the CLR from other runtimes, though, is the fact that it's decoupled from any particular language. Also, the generalization of metadata through custom attributes was quite an innovative feature, as you read much more about throughout this book.

# ## Bootstrapping the Runtime

Previously you saw that executable assemblies are built as EXE files, which as we all know are loaded by the operating system to run them in a separate process. In the pre-.NET world, executable files simply contained native machine instructions that could be understood directly by the processor. Because managed code assemblies require runtime services to execute, a natural question is how the .NET runtime gets loaded when the operating system encounters a managed executable.

For the operating system's loader to recognize the executable file as a valid one, it needs to have a structure that is defined in the PE/COFF file format, which stands for Portable Executable, Common Object File Format. This file format describes the structure of executable files with regard to the code and data sections they contain, in addition to metadata structures describing things such as imported and exported functions. This standardized format is referred to in the CLI as the way to store assemblies in files.

Despite the richness of PE/COFF files, managed executables use just a tiny little bit of its functionality, enough to transfer control to the CLR as soon as the executable starts. This is achieved by emitting a tiny code section in every managed executable (at compile time) that does basically just one thing:

```
```
JMP _CorExeMain
```
```

This jump instruction transfers control to a function called _CorExeMain that lives in the mscoree.dll file under the system32 folder. From that point on, the runtime is in control.

> **REVEALING THE COMMON LANGUAGE RUNTIME ENTRY-POINT**
> 
> The interested reader is invited to use the dumpbin.exe tool that ships with Visual Studio (and is also available in the Windows SDK) to dump the import table of any managed executable using the tool's /imports flag. This will reveal the _CorExeMain entry point being imported from mscoree.dll.

What's this mscoree.dll thing anyway? The acronym stands for Component Object Runtime Execution Engine, where the COR part is a last trace of the days when the runtime was still considered an extension to COM, adding runtime services to make developers' lives easier. Actually, the role of this DLL is very limited: It's really a very tiny shim that knows how to load an appropriate version of the CLR that's capable of executing the application being started. This facilitates side-by-side installations of multiple .NET Framework versions. The decision which runtime to load is based on the metadata embedded in the executable as well as policy configurations that live in the Registry.