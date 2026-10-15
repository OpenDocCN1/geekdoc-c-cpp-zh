| Table 35.2: Noteworthy Public Methods of the AppDomain Class |
| Method | Description |
| CreateInstanceFromAndUnwrap() | Builds a new instance, which is not wrapped, of a specified type, where the source is specified in the specified assembly file |
| ExecuteAssembly() | Executes the assembly contained in the specified file |
| GetAssemblies() | Obtains the assemblies that have been loaded into the application domain |
| GetCurrentThreadId() | Obtains the current thread identifier |
| InitializeLifetimeService() | Starts providing lifetime service to an AppDomain object at the time of its initialization |
| IsFinalizingForUnload() | Indicates whether or not the application domain is unloading, and the objects it contains are being finalized by the CLR |
| Load() | Loads an assembly into the application domain |
| SetAppDomainPolicy() | Establishes a security policy for an application domain |
| SetCachePath() | Sets a directory path to store the copies of assemblies |
| SetShadowCopyFiles() | Turns on shadow-copying |
| Unload() | Unloads the specified application domain |

Table 35.3 lists the noteworthy public events of the AppDomain class:

| Table 35.3: Noteworthy Public Events of the AppDomain Class |
| Event | Description |
| AssemblyLoad | Occurs when an assembly is loaded |
| AssemblyResolve | Occurs when the resolution of an assembly fails |
| DomainUnload | Occurs when an AppDomain is about to be unloaded |
| ProcessExit | Occurs on the default application domain when the default application domain's parent process exits |
| ResourceResolve | Occurs when the resolution of a resource fails |
| TypeResolve | Occurs when the resolution of a type fails |

# Remotable and Non-Remotable Objects

The .NET remoting architecture divides objects into two categories – non-remotable and remotable. An object belongs to the remotable category if and only if instances of the object can cross .NET remoting boundaries or can be accessed by other objects across .NET remoting boundaries. If an object does not satisfy either of these conditions, then the object falls under the category of non-remotable objects. In other words, non-remotable objects are those objects that cannot be accessed outside their own application domains. The non-remotable objects are designed for use within the same AppDomain in which they were created and are always accessed directly from that AppDomain. Furthermore, the non-remotable objects cannot be copied or represented in another AppDomain.

Unlike non-remotable objects, remotable objects are accessible outside their own AppDomain using a proxy. The .NET remoting architecture broadly divides the remotable objects into two categories – marshal-by-value (MBV) and marshal-by-reference (MBR). Let’s discuss these two categories in the following sections.

# Marshal-By-Value

Marshalling is a process of packaging and sending method calls between objects and across application boundaries using the serialization and deserialization mechanisms. The MBV objects declare their serialization