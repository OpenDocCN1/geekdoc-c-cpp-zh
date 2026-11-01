Deployment processes can be complex for a large application. Planning for the deployment can save time and effort when the deployment process is implemented.

Choosing the proper deployment option must be done with the same care and planning as any other aspect of the system being developed. Choosing the wrong option will make the process of getting the software into the users' hands difficult and frustrating.

# Deployment Options

This section provides an overview of the deployment options that are available to .NET developers. Most of these options are discussed in greater detail later in this chapter.

+   - **Xcopy** — The xcopy utility lets you copy an assembly or group of assemblies to an application folder, cutting down on your development time. Because assemblies are self-discovering (that is, the metadata that describes the assembly is included in the assembly), you do not need to register anything in the registry.

Each assembly keeps track of what other assemblies it requires to execute. By default, the assembly looks in the current application folder for the dependencies. The process of moving (or probing) assemblies to other folders is discussed later in this chapter.

+   - **Publishing web sites** — When a web site is published, the entire site is compiled and then copied to a specified location. As a result of precompiling, all source code is removed from the final output and all compile errors can be found and dealt with.

+   - **Deployment projects** — Visual Studio 2010 has the capability to create setup programs for an application. There are four options based on Microsoft Windows Installer technology:
+     - Creating merge modules,
+     - Creating a setup for client applications,
+     - Creating a setup for web applications, and
+     - Creating a setup for Smart Device-based (Compact Framework) applications.

The ability to create cab files is also available. Deployment projects offer a great deal of flexibility and customization for the setup process. One of these deployment options will be useful for larger applications.

+   - **ClickOnce technology** — The ClickOnce technology offers a way to build self-updating Windows-based applications. ClickOnce allows an application to be published to a web site, file share, or even a CD. As updates and new builds are made to the application, they can be published to the same location or site by the development team. As the application is used by the end user, it checks the location to see if an update is available. If there is, an update is attempted.

# Deployment Requirements

It is instructive to look at the runtime requirements of a .NET-based application. The CLR has certain requirements on the target platform before any managed application can execute.