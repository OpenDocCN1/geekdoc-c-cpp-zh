
# Simple Administrative Control (Configuration)

The user or the administrator can determine some aspects of an application's execution. For example, an administrator might decide to move assembly files on the user's hard disk or override information contained in the assembly's manifest. Other scenarios also exist related to versioning; I'll talk about some of these in Chapter 3.

To allow administrative control over an application, a configuration file can be placed in the application's directory. An application's publisher can create and package this file. The setup program would then install this configuration file in the application's base directory. In addition, the machine's administrator or an end user could create or modify this file. The CLR interprets the content of this file to alter its policy for locating and loading assemblies.

These configuration files contain Extensible Markup Language (XML) and can be associated with an application or with a machine. Using a separate file (vs registry settings) allows the file to be easily backed up and also allows the administrator to copy the application to another machine—just copy the necessary files and the administrative policy is copied too.

In Chapter 3, we'll explore this configuration file in more detail. But I want to give you a taste of it now. Let's say that the publisher of an application wants its application deployed with the MultiFile-assembly files in a different directory than the application's assembly file. The desired structure looks like this:

```
AppDir directory (contains the application's assembly files)
Program.exe
Program.exe.config (discussed below)
```

```
Aux subdirectories (contains MultiFileLibrary's assembly files)
MultiFileLibrary.dll
FUT.netmodule
RUT.netmodule
```

Because the MultiFileLibrary files are no longer in the application's base directory, the CLR won't be able to locate and load these files; running the application will cause a System.IO.FileNotFoundException to be thrown. To fix this, the publisher creates an XML configuration file and deploys it to the application's base directory. The name of this must be the name of the application's main assembly file with a .config extension: Program.exe.config, for this example. The configuration file should look like the following:

```
<configuration>
<runtime>
  <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
    <probing privatePath="AuxFiles" />
  </assemblyBinding>
</runtime>
</configuration>
```

When the CLR attempts to locate an assembly file, it always looks in the application's directory first, and if it can't find the file, it looks in the Aux subdirectory. You can specify semicolon-delimited paths for the probingPath attribute. Each path is considered relative to the application's base directory. You cannot specify an absolute or a relative path identifying a directory that is outside of the application's base directory. The idea is that an application can control its directory and its subdirectories but has no control over others.

## Probing for Assembly

When the CLR needs to locate an assembly, it scans several subdirectories. Here is the order in which directories are probed for a culture-neutral assembly (where firstPath and secondPath are specified via the probing attribute):

```
AppDir\AssemblyName.dll
AppDir\AssemblyName.dll
AppDir\firstPath\AssemblyName.dll
AppDir\firstPath\AssemblyName.dll
AppDir\secondPath\AssemblyName.dll
AppDir\secondPath\AssemblyName.dll
```

In this case, no configuration file was deployed to a subdirectory called MultiFileLibrary because the CLR would automatically scan for a subdirectory whose name matches that of the assembly being searched.

If the assembly can't be found in any of the preceding subdirectories, the CLR will start over using an .exe extension instead of .dll. If the assembly still can't be found, a FileNotFoundException is thrown.

For satellite assemblies similar rules are followed except that the assembly is expected to be in a subdirectory whose name matches the culture of the application's base directory. For example, if the culture "en-US" is applied to it, the following directories are probed:

```
AppDir\en-US\AssemblyName.dll
AppDir\en-US\AssemblyName.dll
AppDir\firstPath\en-US\AssemblyName.dll
AppDir\firstPath\en-US\AssemblyName.dll
AppDir\secondPath\en-US\AssemblyName.dll
AppDir\secondPath\en-US\AssemblyName.dll
```

```
AppDir\en-US\AssemblyName.exe
AppDir\en-US\AssemblyName.exe
AppDir\firstPath\en-US\AssemblyName.exe
AppDir\firstPath\en-US\AssemblyName.exe
AppDir\secondPath\en-US\AssemblyName.exe
AppDir\secondPath\en-US\AssemblyName.exe
```

As you can see, the CLR probes for files with either .exe or .dll extension. Because probing can be very time-consuming (especially when the CLR is looking for files over a network), in the XML configuration file you can specify one or more culture elements to limit the probing the CLR performs when looking for satellite assemblies. Microsoft provides a FusLog tool you can use to see how the CLR is binding to assemblies at run. For more information about it, see http://msdn.microsoft.com/en-us/library/e7a18c4(v=vs.8).aspx.

The name and location of this XML configuration file is different depending on the application type:

- For executable applications (EXEs), the configuration file must be in the application's directory, and it must be the name of the EXE file with ".config" appended to it.
- For Microsoft ASP.NET Web Forms, the file must be in the Web application's virtual root directory and is always named Web.config. In addition, subdirectories also contain their own Web.config file, and the configuration settings are inherited. For example, a Web application located at http://example.com/Training would use the settings in the Web.config files contained in the virtual root directory and in its Training subdirectory.

As mentioned at the beginning of this section, configuration settings apply to a particular application and to the machine. When you install the .NET Framework, it creates a Machine.config file. There is one Machine.config file per version of the CLR you have installed on the machine.

The Machine.config file is located in the following directory:

```
%SystemRoot%\Microsoft.NET\Framework\version\CONFIG
```

Settings in the Machine.config file define settings that all applications running on the machine. An administrator can create a machine-wide policy by modifying the Machine.config file. However, administrators and users should avoid modifying this file because it contains many settings related to various things which makes it much more difficult to navigate. Plus, you want the application's settings to be backed up and restored, and keeping them in the application-specific configuration file enables this.
