
Now, when using the FancyCalculator type from any .NET language, we don't know that its Add method was implemented in a different language than its Multiply method. To illustrate the seamless integration the unified type system offers, let's use our library from inside F#'s interactive console. This is shown in Figure 1.8.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_61_0.png)

FIGURE 1.8 Using our multilanguage calculator type in F#.

Figure 1.9 summarizes the development flow we've gone through to enable this scenario.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_61_1.png)

FIGURE 1.9 Developing and using code in multiple languages.

## Diving into the Common Language Runtime

Now that you know how assemblies are built, the time has come to focus on the runtime infrastructure the CLR offers. Actually, the concept of a runtime wasn't groundbreaking at the time the CLR was introduced: Languages such as Visual Basic have had them for years, and so did Java with its virtual machine (JVM). What distinguishes the CLR from other runtimes, though, is the fact that it's decoupled from any particular language. Also, the generalization of metadata through custom attributes was quite an innovative feature, as you read much more about throughout this book.

### Bootstrapping the Runtime

Previously you saw that executable assemblies are built as EXE files, which as we all know are loaded by the operating system to run them in a separate process. In the pre-.NET world, executable files simply contained native machine instructions that could be understood directly by the processor. Because managed code assemblies require runtime services to execute, a natural question is how the .NET runtime gets loaded when the operating system encounters a managed executable.

For the operating system's loader to recognize the executable file as a valid one, it needs to have a structure that is defined in the PE/COFF file format, which stands for Portable Executable, Common Object File Format. This file format describes the structure of executable files with regard to the code and data sections they contain, in addition to metadata structures describing things such as imported and exported functions. This standardized format is referred to in the CLI as the way to store assemblies in files.

Despite the richness of PE/COFF files, managed executables use just a tiny little bit of its functionality, enough to transfer control to the CLR as soon as the executable starts. This is achieved by emitting a tiny code section in every managed executable (at compile time) that does basically just one thing:

```
JMP _CorExeMain
```

This jump instruction transfers control to a function called _CorExeMain that lives in the mscoree.dll file under the system32 folder. From that point on, the runtime is in control.

> **REVEALING THE COMMON LANGUAGE RUNTIME ENTRY-POINT**
> 
> The interested reader is invited to use the dumpbin.exe tool that ships with Visual Studio (and is also available in the Windows SDK) to dump the import table of any managed executable using the tool's /imports flag. This will reveal the _CorExeMain entry point being imported from mscoree.dll.

What's this mscoree.dll thing anyway? The acronym stands for Component Object Runtime Execution Engine, where the COR part is a last trace of the days when the runtime was still considered an extension to COM, adding runtime services to make developers' lives easier. Actually, the role of this DLL is very limited: It's really a very tiny shim that knows how to load an appropriate version of the CLR that's capable of executing the application being started. This facilitates side-by-side installations of multiple .NET Framework versions. The decision which runtime to load is based on the metadata embedded in the executable as well as policy configurations that live in the Registry.

### NOTE

Beginning with Windows XP, the operating system’s executable loader has some limited built-in knowledge of the common language runtime to redirect the execution of a managed executable to the runtime as early as possible. Nowadays, various built-in services, such as Windows Installer, have intrinsic knowledge about the existence of managed assemblies. Starting with Windows Vista, parts of the .NET Framework are an integral part of the operating system installation to facilitate services that depend on them.

Once the shim knows what version of the runtime to load, it goes ahead and locates the real execution engine DLL for the selected version of the runtime. The version-specific runtime components live in folders underneath the %windir%\\Microsoft.NET folder. In .NET 2.0, the runtime DLL was called mscorwks.dll, which stands for Component Object Runtime Workstation, another historical naming that reflects there once were multiple flavors of the runtime. (One flavor was optimized to run on servers, while another was optimized to run on clients or workstations, the main difference being different GC behavior.) Today, this distinction is more configurable, and no separate DLLs are required, so .NET 4.0’s execution engine lives in a more logically named file, clr.dll.

### NOTE

Keeping shims as tiny as possible is not always an easy thing to do. It sounds more than logical that no version-specific runtime functionality should live in the shim, but in practice that turns out to be a challenge. In .NET 4.0, the original shim has been trimmed down to make it more future-proof. This refactoring made mscoree.dll into a super-shim, with the remainder functionality moved to a new DLL called mscoreei.dll. This way, the need to update mscoree.dll every time an update to the .NET Framework is applied should decrease significantly.

One of the first things the runtime does after it has gained control over the execution of a managed executable is to inspect the PE/COFF headers looking for a CLR-specific header that specifies a pointer into the metadata directory of the assembly. Such a header is illustrated here:

```
clr Header:

                 48 cb
              2.05 runtime version
                 20AC [       304] RVA [size] of MetaData Directory
                             1 flags
                                IL Only

         6000001 entry point token
```

Locating the entry point token through the metadata directories, the runtime now has all the required information to locate the application’s entry point method and start

## Cash Flow Statement

For the years ended December 31,

| | 2023 | 2022 | 2021 |
| --- | ---: | ---: | ---: |
| **Cash flows from operating activities** | | | |
| Net income | 1,200,000 | 980,000 | 850,000 |
| Adjustments to reconcile net income to net cash provided by operating activities: | | | |
| Depreciation and amortization | 150,000 | 140,000 | 130,000 |
| Stock-based compensation | 45,000 | 40,000 | 35,000 |
| Changes in operating assets and liabilities: | | | |
| Accounts receivable | (30,000) | (25,000) | (20,000) |
| Inventory | (18,000) | 12,000 | (8,000) |
| Accounts payable | 22,000 | (5,000) | 15,000 |
| Accrued expenses | 10,000 | 8,000 | (6,000) |
| **Net cash provided by operating activities** | **1,379,000** | **1,150,000** | **996,000** |
| **Cash flows from investing activities** | | | |
| Purchases of property and equipment | (350,000) | (280,000) | (220,000) |
| Proceeds from sale of equipment | 25,000 | 15,000 | 10,000 |
| **Net cash used in investing activities** | **(325,000)** | **(265,000)** | **(210,000)** |
| **Cash flows from financing activities** | | | |
| Proceeds from issuance of common stock | 100,000 | 50,000 | 80,000 |
| Repayment of long-term debt | (200,000) | (150,000) | (100,000) |
| Dividends paid | (80,000) | (75,000) | (60,000) |
| **Net cash used in financing activities** | **(180,000)** | **(175,000)** | **(80,000)** |
| **Net increase in cash and cash equivalents** | **874,000** | **710,000** | **706,000** |
| Cash and cash equivalents, beginning of year | 1,250,000 | 540,000 | (166,000) |
| **Cash and cash equivalents, end of year** | **2,124,000** | **1,250,000** | **540,000** |
