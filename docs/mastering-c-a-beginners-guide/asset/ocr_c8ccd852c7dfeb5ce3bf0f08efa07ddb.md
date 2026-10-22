An assembly reference list is, in essence, a list of all external dependencies, such as .dlls or other files. Assembly references include references to both global and private objects. Global objects are accessible to all other applications. In .NET Core, global objects are coupled with a particular .NET Core runtime. In .NET Framework, global objects house in the GAC. System.IO.dll is a perfect example of an assembly in the GAC. Private objects must be in a directory level at or below the directory in which your app is installed.

# What Are the Benefits of Using Assemblies?

Assemblies are mainly introduced to sort out the problems of versioning, DLL conflicts, and simplifying deployment. Most end users have experienced versioning or deployment issues when installing a new version or a new application of an existing one. There are many circumstances where you install a new application only to find an existing one stopped working, and the system cannot recover from that. Many developers spent much of their time retaining the registry entries consistency to activate a COM class. All this frustration happens because of versioning issues that occur with component-based applications.

# Versioning Problems

Two versioning problems occur with WIN32 applications. The versioning rules are enforced by the OS and are not between the pieces of an application. Backward compatibility between the new part of code and the old one is the current way of versioning, and this is almost impossible to maintain in most applications. Besides that, only a single