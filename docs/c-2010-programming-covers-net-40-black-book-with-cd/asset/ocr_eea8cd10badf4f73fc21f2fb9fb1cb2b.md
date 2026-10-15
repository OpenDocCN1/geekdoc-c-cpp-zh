# ## Assembly Information File

You have learned about the manifest of an assembly, which is the most important component of any assembly. Now let’s see from where the manifest gets most of its information. Every project that is created by using Visual C# has an AssemblyInfo.cs file, which has a lot of configuration attributes and other information, such as the company name, version, trademark information, and assembly name. The assembly information file uses these configuration attributes to assign strong key and specify additional information to an assembly, such as company name, version, and assembly name.

Listing 33.1 displays the code of the AssemblyInfo.cs file of an application:

# Listing 33.1: Showing the Code of the Assembly Information File

```
```csharp
...
[assembly: AssemblyKeyFile("Akey.snk")]
[assembly: AssemblyTitle("SharedObject")]
[assembly: AssemblyDescription("")]
[assembly: AssemblyConfiguration("")]
[assembly: AssemblyCompany("Kogent Solutions Inc")]
[assembly: AssemblyProduct("SharedObject")]
[assembly: AssemblyCopyright("Copyright © Kogent Solutions Inc 2010")]
[assembly: AssemblyTrademark("")]
[assembly: AssemblyCulture("")]

// Major Version
// Minor Version
// Build Number
// Revision
...
[assembly: AssemblyVersion("1.0.0.0")]
...
```
```

# ## Version Format

The AssemblyInfo.cs file contains a comment that specifies the format of the assembly version. Following syntax shows the format of the assembly version:

```
```text
<Major Version>.<Minor Version>.<Build Number>.<Revision>
```
```

In the preceding syntax, Build Number and Revision number change if the changes made in the assembly are not major. A major change, such as removing or changing the functionality that renders the assembly incompatible with the older version, can be reflected by changing the major versions. The version information is specified by the AssemblyVersion attribute as you can see in Listing 33.1.

# ## Configuration Files for Assemblies

You can redirect a client to use the new version of an assembly without building the client again. However, you must first configure the client in the .NET Framework 2.0 Configuration tool. The .NET Framework 2.0 Configuration tool creates a configuration file with an extension .exe.config, when we configure the client through it. This configuration file contains the code, which indicates that the client is redirected to the new version of the current assembly, as shown in Listing 33.2:

# Listing 33.2: Showing the Code of the Configuration Files for Assemblies

```
```xml
<?xml version="1.0"?>
<configuration>
    ......
        <bindingRedirect oldVersion="1.0.0.0" newVersion="1.1.0.0" />
    ......
```
```