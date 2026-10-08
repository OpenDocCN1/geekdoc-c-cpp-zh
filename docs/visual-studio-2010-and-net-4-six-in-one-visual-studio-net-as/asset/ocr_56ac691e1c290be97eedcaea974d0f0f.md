The Package class elements implement the IVsPackage interface required by Visual Studio to take an object account as a package. This interface provides a few methods managing the life cycle of a package and offers methods to access package-related objects such as tool windows, options pages, and authentication objects.

 overridden Initialize method is called after the package has been successfully sited in the Shell through the IVsPackage interface. This method must do all the initialization steps that require access to services provided by the Shell or other packages. You should move this code to the package constructor, you probably would get a NullReferenceException,, at point, all attempts to access the Shell would fail because the package is not yet sited, and has no contact with any Shell objects.

In this case, the Initialize method binds the single menu command provided by the package with its event handler method called MenuItemCallback:

```
protected void Initialize()
{
    Trace.WriteLine(string.Format(CultureInfo.CurrentCulture, "Entering Initialize() of: {0}", this.ToString()));
    base.Initialize();

n    // Add our command handlers for the menu (commands must exist in the .vsct file)
    OleMenuCommandService mcs = GetService(typeof(IMenuCommandService))
        as OleMenuCommandService;
    if (mcs != null)
    {
        // Create the menu item.
        CommandID menuCommandID = new CommandID(Guid.Guid.GuidSimplePackageCmdSet,
            (int)PkgCmdIDList.mdIDExecuteSimpleCommand);
        MenuCommand menuItem = new MenuCommand(MenuItemCallback, menuCommandID);
        mcs.AddCommand(menuItem);
    }
}
```

First, call the Initialize method of the base class — Package, in this case. Look at all of GetService. If you could select a method that is especially important when creating Visual Studio packages, the GetService method would be your choice. This method has one type parameter (call it service) that retrieves a service object implementing the service interface specified by the address type.

You obtain an OleMenuCommandService instance that you create a CommandID instance to address the command you put into the Tools menu, and then you instantiate a MenuCommand object to address the MenuItemCallback method as a response for the command specified with the CommandID. The result of this short initialization code is that the package handles when the user clicks on the Sample Command item in the Tools menu by executing the MenuItemCallback method, which uses the IVUIService to serve up a message box from the IDE.

As mentioned, packages are COM objects that are registered with Visual Studio to support the on-demand loading mechanism and allow merging menus and toolbars into the user interface of