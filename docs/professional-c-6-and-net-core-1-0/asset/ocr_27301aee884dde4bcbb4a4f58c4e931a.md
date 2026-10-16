design view with Visual Studio and then selecting the Add Installer option from the context menu . With this option, a new `ProjectInstaller` class is created, along with a `ServiceInstaller` instance and a `ServiceProcessInstaller` instance.

Figure 39.9 shows the class diagram of the installer classes for services.

Keep this diagram in mind as we go through the source code in the file `ProjectInstaller.cs` that was created with the Add Installer option.

# The Installer Class

The class `ProjectInstaller` is derived from `System.Configuration.Install.Installer`. This is the base class for all custom installers. With the `Installer` class, it is possible to build transaction-based installations. With a transaction-based installation, you can roll back to the previous state if the installation fails, and any changes made by this installation up to that point will be undone. As shown in Figure 39.9, the `Installer` class has `Install`, `Uninstall`, `Commit`, and `Rollback` methods, and they are called from installation programs.

![](bbox=[0.105, 0.413, 0.895, 0.843])

Figure 39.9

The attribute `[RunInstaller(true)]` means that the class `ProjectInstaller` should be invoked when installing an assembly. Custom action installers, as well as `installutil.exe` (which is used