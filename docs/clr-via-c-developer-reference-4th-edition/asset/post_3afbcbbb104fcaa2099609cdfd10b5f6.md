
Furthermore, because the /out:Program.exe and the /t:exe command-line switches also match the C# compiler would choose as defaults, the following command line gives the same results too.

csc.exe Program.cs

If, for some reason, you really don't want the C# compiler to reference the MSCor.dll assembly, you can use the /nostdlib switch. Microsoft uses this when building the MSCorLib.dll assembly itself. For example, the following command line will generate an error when CSC.exe attempts to compile the Program.cs file because the System.Console type is defined in MSCorLib.dll.

csc.exe /out:Program.exe /t:nostdlib Program.cs

Now, let's take a closer look at the Program.exe file produced by the C# compiler. What exactly is this file? For starters, it is a standalone executable (PE) file. This means that a machine running 32-bit or 64-bit versions of Windows would be able to load this and do something with. Windows supports three types of applications. To build a console user interface (CUI) application, specify the /t:exe switch; to build a graphical user interface (GUI) application, specify the /t:winex switch; and to build a Windows Store app, specify the /t:apparenterexe switch.

## Response Files

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

When you install the .NET Framework, it installs a default global CSC file in the %SystemRoot%\Microsoft\.Framework\(v64)\X.X.X directory where X.X.X is the version of the .NET Framework with installed. The latest version of this file contains the following switches:

```
# This file contains command-line options that the C# command line compiler CSC will process as part
# of every compilation, unless the "/config" option
# is specified.

# Reference the common Framework libraries
#r:/Accessibility.dll
#r:/Microsoft.Sharp.dll
#r:/System.Configuration.dll
#r:/System.Configuration.Install.dll
#r:/System.Core.dll
#r:/System.Data.dll
#r:/System.Data.DataSetExtensions.dll
#r:/System.Data.Linq.dll
#r:/System.Data.OracleClient.dll
#r:/System.Deployment.dll
#r:/System.Design.dll
#r:/System.DirectoryServices.dll
#r:/System.dll
#r:/System.Drawing.Design.dll
#r:/System.Drawing.dll
#r:/System.EnterpriseServices.dll
#r:/System.Management.dll
#r:/System.Messaging.dll
#r:/System.Runtime.Remoting.dll
#r:/System.Runtime.Serialization.dll
#r:/System.Runtime.Serialization.Formatters.Soap.dll
#r:/System.Security.dll
#r:/System.ServiceModel.dll
#r:/System.ServiceModel.Web.dll
#r:/System.ServiceProcess.dll
#r:/System.Transactions.dll
#r:/System.Web.dll
#r:/System.Web.Extensions.Design.dll
#r:/System.Web.Extensions.dll
#r:/System.Web.Mobile.dll
#r:/System.Web.RegularExpressions.dll
#r:/System.Web.Services.dll
#r:/System.Windows.Forms.dll
#r:/System.Workflow.Activities.dll
#r:/System.Workflow.ComponentModel.dll
#r:/System.Workflow.Runtime.dll
#r:/System.Xml.dll
#r:/System.Xml.Linq.dll
```

Because the global CSC.file references all of the assemblies listed, you do not need to explicitly reference these assemblies by using the C# compiler's /reference switch. This response file is a big convenience for developers it allows them to use types and namespaces defined in Microsoft-published assemblies without having to specify a /reference compiler switch for each when compiling.

Referencing all of these assemblies could slow the compiler a bit. But if your source code doesn't refer to a type or member defined by any of these assemblies, there is no impact on the re-assembling file, nor to run-time execution performance.

When you use the /reference compiler switch to reference an assembly, you can specify a complete path to a particular file. However, if you do not specify a path, the compiler will search for the file in the following places (in the order listed):

- Working directory.
- The directory that contains the CSC.exe file itself. MSCorLib.dll is always obtained from this directory. The path looks something like this: %SystemRoot%\Microsoft\.NET\Framework\v4.0.XXXX.
- Any directories specified using the /lib compiler switch.
- Any directories specified using the LIB environment variable.

Of course, you're welcome to add your own switches to the global CSC.rsp file if you want to make your life even easier, but this makes it more difficult to replicate the build environment on different machines—you have to remember to update the CSC.rsp on each build machine. Also, you can tell the compiler to ignore both local and global CSC.rsp files by specifying the /noconfig command-line switch.

## A Brief Look at Metadata

Now we know what kind of PE file we've created. But what exactly is in the Program.exe file? A managed PE file has four main parts: the PE32(+) header, the CLR header, the metadata, and the IL. The PE32(+) header is the standard information that Windows expects. The CLR header is a small block of information that is specific to modules that require the CLR (managed modules). The header includes the major and minimum version of the CLR that the module was built for: some flags, a MethodDef indicating the module's entry point if this module is a GUI, Console, an optional strong-name digital signature (discussed in Chapter 3). Finally, the header contains the size and offsets of metadata tables contained within the module. You can see the exact format of the CLR header by examining the IMAGE_COR20_HEADER defined in the CorHdr header file.

The metadata is a block of binary data that consists of several tables. There are three categories of tables: definition tables, reference tables, and manifest tables. Table 2-1 describes some of the common definition tables that exist in a module's metadata block.

### TABLE 2-1 Common Definition Tables

| Metadata Definition Table Name | Description |
| :--- | :--- |
| ModuleDef | Always contains one entry that identifies the module. The entry includes the module's file name and extension (without path) and a module version ID (in the form of GUID created by the compiler). |
| TypeDef | Contains one entry for each type defined in the module. Each entry includes the type's name, base type, and flags (public, private, etc.) and contains indexes to the methods in the MethodDef table, the properties in the FieldDef table, the events in the EventDef table. |
| MethodDef | Contains one entry for each method defined in the module. Each entry includes the method's name, flags (private, public, virtual, abstract, static, final, etc.), signature and offset within the module where its IL code can be found. Each entry can refer to a ParamDef table in which more information about the method's parameters can be found. |
| FieldDef | Contains one entry for every field defined in the module. Each entry includes flags (private, public, etc.), type, and name. |
| ParamDef | Contains one entry for each parameter defined in the module. Each entry includes flags (in, out, retval, etc.), type, and name. |
| PropertyDef | Contains one entry for each property defined in the module. Each entry includes flags, type, and name. |
| EventDef | Contains one entry for each event defined in the module. Each entry includes flags and name. |

As the compiler compiles your source code, every code defines an entry to be created in one of the tables described in Table 2-1. Metadata table entries are also created as the compiler detects the types, fields, methods, properties, and events that the source code references. The metadata created a set of reference tables to keep a record of the referenced items. Table 2-2 shows some of the most common reference metadata tables.

### TABLE 2-2 Common Reference Metadata Tables

| Metadata Reference Table Name | Description |
| :--- | :--- |
| AssemblyRef | Contains one entry for each assembly, referenced by the module. Each entry includes the information needed to bind to the assembly: the assembly name (without path and extension), version number, culture, and public key token (normally a hash value generated from the publisher's public key, identifying the referenced assembly's publisher). Each entry also contains some flags and a hash value. This hash value is intended to be a checksum of the referenced assembly's bits. The CLR completely ignores this hash value and will probably to do so in the future. |
| ModuleRef | Contains one entry for each PE module that implements types referenced by this module. Each entry includes the module's file name and extension (without path). This table is used to bind to types that are implemented in different modules of the calling assembly's module. |
