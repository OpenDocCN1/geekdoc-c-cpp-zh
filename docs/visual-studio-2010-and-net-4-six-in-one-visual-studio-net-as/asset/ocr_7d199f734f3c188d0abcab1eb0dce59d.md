compatible with older versions, and a concrete CLR could run applications developed with any of the preceding versions. In this way, .NET Framework versions could be seamlessly updated to a newer one so that only one (the latest) version is installed on a computer, while being able to run the applications originally targeting an old framework version.

# Understanding Side-By-Side Execution

This approach has serious limitations. Aiming at full compatibility would mean that any design issues, mistakes, or paradigm decisions should show in the framework forever. This simply does not work, it is a very strict limit for innovations! Full compatibility means not only that all source code will compile with all new framework versions, but also documented and undocumented behaviors remain the same. It would mean, even if you have multiple CPU cores in them, any existing framework implementation would be allowed to leverage on this capability implicitly, because of backward compatibility issues, as .NET Framework 1.0 BCL was designed with single CPU core in mind.

The CLR avoided the "one-CLR rules" and designed the .NET Framework from the very first version with the capability to run separate versions side-by-side on the same computer. This is a good approach from the point of view that it prevents the "innovation bottleneck.". However, the side-by-side scenario avoids an important question of which CLR version an application or a component should use the ones installed on the machine.

# Issues Before CLR 4.0

.NET Framework was designed to run the application with the CLR with which it was built. Well, this works well for managed applications. The CLR loads into the process space of the application, and that simply works. However, when the original CLR is not present, the application must run with another version of the CLR that is automatically the latest version installed on the computer.

There are issues with managed COM components used by native applications (like Word, Excel, Outlook, or other applications expecting COM extensions). If the native application tries to load two managed components with separate CLRs, it cannot be done. Only one CLR version can be loaded into an operating system process, which always has to be the latest

# .NET 4 Changes in CLR Hosting

CLR 4.0 provides a new approach to side-by-side hosting. The installation of a new .NET Framework has no effect on existing applications. Managed applications and the add-ins they do run against the version of the .NET Framework with which they were built. And in contrast to the preceding versions, the applications do not automatically use the latest .NET Framework installed on the machine, unless explicitly to do so.

Native applications can now host managed COM components built and tested with separate CLRs. The process can host more CLR versions side-by-side, and so each COM component can run with the CLR version with which it was registered.