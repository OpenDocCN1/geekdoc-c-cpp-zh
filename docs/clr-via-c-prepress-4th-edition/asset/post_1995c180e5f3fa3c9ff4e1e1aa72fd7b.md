
## The Native Code Generator Tool: NGen.exe

The NGen.exe tool that ships with the .NET Framework can be used to compile IL code to native code when an application is installed on a user’s machine. Since the code is compiled at install time, the CLR’s JIT compiler does not have to compile the IL code at runtime, and this can improve the application’s performance. The NGen.exe tool is interesting in two scenarios:

- **Improving an application’s startup time** Running NGen.exe can improve startup time because the code will already be compiled into native code so that compilation doesn’t have to occur at runtime.
- **Reducing an application’s working set** If you believe that an assembly will be loaded into multiple processes simultaneously, running NGen.exe on that assembly can reduce the application’s working set. The reason is because the NGen.exe tool compiles the IL to native code and saves the output in a separate file. This file can be memory-mapped into multiple-process address spaces simultaneously, allowing the code to be shared; not every process needs its own copy of the code.

When a setup program invokes NGen.exe on an application or a single assembly, all of the assemblies for that application or the one specified assembly have their IL code compiled into native code. A new assembly file containing only this native code instead of IL code is created by NGen.exe. This new file is placed in a folder under the directory with a name like %SystemRoot%\Assembly\NativeImages_v4.0.#####_64. The directory name includes the version of the CLR and information denoting whether the native code is compiled for 32-bit or 64-bit versions of Windows.

Now, whenever the CLR loads an assembly file, the CLR looks to see if a corresponding NGen’d native file exists. If a native file cannot be found, the CLR JIT compiles the IL code as usual. However, if a corresponding native file does exist, the CLR will use the compiled code contained in the native file, and the file’s methods will not have to be compiled at runtime.

On the surface, this sounds great! It sounds as if you get all of the benefits of managed code (garbage collection, verification, type safety, and so on) without all of the performance problems of managed code (JIT compilation). However, the reality of the situation is not as rosy as it would first seem. There are several potential problems with respect to NGen’d files:

- **No intellectual property protection** Many people believe that it might be possible to ship NGen’d files without shipping the files containing the original IL code, thereby keeping their intellectual property a secret. Unfortunately, this is not possible. At runtime, the CLR requires access to the assembly’s metadata (for functions such as reflection and serialization); this requires that the assemblies that contain IL and metadata be shipped. In addition, if the CLR can’t use the NGen’d file for some reason (described below), the CLR gracefully goes back to JIT compiling the assembly’s IL code, which must be available.
- **NGen’d files can get out of sync** When the CLR loads an NGen’d file, it compares a number of characteristics about the previously compiled code and the current execution environment. If any of the characteristics don’t match, the NGen’d file cannot be used, and the normal JIT compiler process is used instead. Here is a partial list of characteristics that must match:
    - CLR version: this changes with patches or service packs
    - CPU type: this changes if you upgrade your processor hardware
    - Windows OS version: this changes with a new service pack update
    - Assembly’s identity module version ID (MVID): this changes when recompiling
    - Referenced assembly’s version IDs: this changes when you recompile a referenced assembly
    - Security: this changes when you revoke permissions (such as declarative inheritance, declarative link-time, SkipVerification, or UnmanagedCode permissions) that were once granted

**Note** It is possible to run NGen.exe in update mode. This tells the tool to run NGen.exe on all of the assemblies that had previously been NGen’d. Whenever an end user installs a new service pack of the .NET Framework, the service pack’s installation program will run NGen.exe in update mode automatically so that NGen’d files are kept in sync with the version of the CLR installed.

- **Inferior execution-time performance** When compiling code, NGen can’t make as many assumptions about the execution environment as the JIT compiler can. This causes NGen.exe to produce inferior code. For example, NGen won’t optimize the use of certain CPU instructions; it adds indirections for static field access because the actual address of the static fields isn’t known until runtime. NGen inserts code to call class constructors everywhere because it doesn’t know the order in which the code will execute and if a class constructor has already been called. (See Chapter 8, "Methods," for more about class constructors.) Some NGen’d applications actually perform about 5 percent slower when compared to their JIT-compiled counterpart. So, if you’re considering using NGen.exe to improve the performance of your application, you should compare NGen’d and non-NGen’d versions to be sure that the NGen’d version doesn’t actually run slower! For some applications, the reduction in working set size improves performance, so using NGen can be a net win.

Due to all of the issues just listed, you should be very cautious when considering the use of NGen.exe. For server-side applications, NGen.exe makes little or no sense because only the first client request experiences a performance hit; future client requests run at high speed. In addition, for most server applications, only one instance of the code is required, so there is no working set benefit.

For client applications, NGen.exe might make sense to improve startup time or to reduce working set if an assembly is used by multiple applications simultaneously. Even in a case in which an assembly is not used by multiple applications, NGen’ing an assembly could improve working set. Moreover, if

| Namespace | Description of Contents |
|---|---|
| System.IO | Types for doing stream I/O and walking directories and files |
| System.Net | Types that allow for low-level network communications and working with some common Internet protocols. |
| System.Runtime.InteropServices | Types that allow managed code to access unmanaged OS platform facilities such as COM components and functions in Win32 or custom DLLs |
| System.Security | Types used for protecting data and resources |
| System.Text | Types to work with text in different encodings, such as ASCII and Unicode |
| System.Threading | Types used for asynchronous operations and synchronizing access to resources |
| System.Xml | Types used for processing Extensible Markup Language (XML) schemas and data |

This book is about the CLR and about the general types that interact closely with the CLR. So the content of this book is applicable to all programmers writing applications or components that target the CLR. Many other good books exist that cover specific application types such as Web Services, Web Forms/MVC, Windows Presentation Foundation, etc. These other books will give you an excellent start at helping you build your application. I tend to think of these application-specific books as helping you learn from the top down because they concentrate on the application type and not on the development platform. In this book, I’ll offer information that will help you learn from the bottom up. After reading this book and an application-specific book, you should be able to easily and proficiently build any kind of application you desire.

## The Common Type System

By now, it should be obvious to you that the CLR is all about types. Types expose functionality to your applications and other types. Types are the mechanism by which code written in one programming language can talk to code written in a different programming language. Because types are at the root of the CLR, Microsoft created a formal specification—the Common Type System (CTS)—that describes how types are defined and how they behave.

**Note** In fact, Microsoft has been submitting the CTS as well as other parts of the .NET Framework, including file formats, metadata, IL, and access to the underlying platform (P/Invoke) to ECMA for the purpose of standardization. The standard is called the Common Language Infrastructure (CLI) and is the ECMA-335 specification. In addition, Microsoft has also submitted portions of the FCL, the C#
