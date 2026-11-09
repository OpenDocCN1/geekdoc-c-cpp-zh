To make sure that security is active, do the following:

+   1. Start MTS Explorer.
+   2. In the left pane, open the Packages Installed folder under My Computer.
+   3. Right-click the System package, and then select Properties.
+   4. Click the Security tab, and then select the Enable Authorization Checking check box.

By default, your MTS Explorer is set to view only the properties for the current computer. However, you can administer another computer’s MTS settings on a network through a single computer.

To view another computer in MTS Explorer, do the following:

+   1. Right-click the Computers folder, point to New, and then select Computer.
+   2. In the Add Computer dialog box, type the name of the computer that you want to administer and click OK. You must have access to this computer, and you must be a member of Reader to view settings, or Administrator to change properties.

> **Note**
> 
> You cannot remotely administer a computer running Windows 95 from a computer running Windows NT.

# Administering Your MTS Server Programmatically

MTS provides a series of scriptable objects that allow you to administer your server programmatically. These objects are based on IDispatch and, although it is definitely possible to use Visual C++ to write programs to use these objects, most people agree that using the IDispatch interface is best left to scripting clients. The MTS administration objects are as follows:

+   - Catalog Root object—Allows you to connect to a local or remote catalog and retrieve a collection
+   - CatalogObject—Allows you to get and set object properties
+   - CatalogCollection—Enumerates, adds, deletes, and modifies catalog objects
+   - PackageUtil—Allows you to install and export a package
+   - ComponentUtil—Installs a component in a specific collection and imports components registered as in-process servers