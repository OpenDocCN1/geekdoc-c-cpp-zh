| Table 33.2: Showing the Manifest Directives |
| Directive | Description |
| .ver <version number> | Determines the referenced assembly's version number |
| .assembly <assembly name> | Determines the name of the assembly |
| .hash algorithm <int32 value> | Determines the hash algorithm used in the assembly |
| .ver <version number> | Determines the assembly's version number |
| .module <file name> | Determines the names of the modules of the assembly |
| .subsystem <value> | Determines the application environment required for the corresponding program to execute |
| .corflags | Represents a reserved field in the metadata |

You can add or change the information stored in the assembly manifest by using assembly attributes in the AssemblyInfo.cs file.

# MSIL Source Code

While compiling an assembly, the compiler translates the source code in MSIL. This is because the MSIL is a platform- and CPU-independent set of instructions that can be executed in any environment supporting .NET Framework. MSIL holds information for loading, storing, initializing, and calling methods on objects as well as instructions to perform various operations, such as arithmetic and logical operations, control flow, direct memory access, and exception handling. As soon as the source code is executed, the Just-in-time (JIT) compiler converts the MSIL to the CPU-specific code.

# Type Metadata

The type metadata describes the format of the types that are stored in an assembly. It also contains the information about the external types that are referenced by the assembly. After executing the code, the CLR loads this metadata to memory and references it to retrieve information about the classes, members, and inheritance of the source code.

# Resources

The .NET Framework localization model consists of a main assembly that contains numerous embedded resources, such as application icons, image files, sound clips, and string tables. As the main assembly contains the embedded resources, if a resource is not found in the localized satellite assembly, the ResourceManager class loads it in a hierarchical manner by falling back to the resource in the main assembly. The .Net Framework also supports satellite assemblies that contain only the localized resources. Satellite assemblies are useful when you want to partition your resources for developing international software based on a specific culture.

# Types of Assemblies

Depending upon their location and accessibility to the clients, assemblies can be broadly categorized as shared or private. A single copy of a shared assembly, stored on a single machine, can be used by several applications. A shared assembly is not deployed within the directory of the application that is using it; instead, it is deployed in the Global Assembly Cache (GAC), which is the storage repository for the assemblies. You can also make an assembly private. This implies that an assembly that is copied to the application's directory can only be accessed by the specified application and no other application can use the same assembly. In other words, if there are only a few applications that need to use your library assembly, you can put them in the relevant application's directory instead of putting them in GAC. As the private assemblies work independently, they are easier to manage and maintain compared to the shared assemblies. The private assemblies do not need strong names and can be installed and uninstalled without any fear of affecting other applications.

When you create an assembly, the LocalCopy property is set to True, by default; which means any assembly that is referenced by a client assembly is copied locally to the client application's directory. In other words, any