+   3. Right-click the Packages Installed branch, point to New on the shortcut menu, and then click Package. The Package Wizard dialog box appears.
+   4. Click the Create An Empty Package button. (You will learn how the Install Pre-Built Packages button is used in the "Importing a Package" section later in this chapter.)
+   5. Type a name for the new package (the name can include spaces). Click Next.
+   6. Set the package identity. You can change the identity later in the Package. During development, you want to use the Interactive User. This setting uses the credentials of the logged on user. A side effect of using the Interactive User is that all output appears in the current WinStation. A problem with this setting is that it requires someone to be logged on for the package to execute.
+   7. In a production environment, you should select the This User option. When you select This User, you can type in a particular user's credentials, which will be implemented when the server needs to access shared resources such as files. Be aware that you should never display output with this setting. The output will not appear in the current WinStation. For example, if you attempt to display a message box, the message would not be visible and your program will appear frozen as it waits for user interaction.
+   8. Click Finish.

# ## Adding Objects to a Package

Although you can add objects to a package using a variety of mechanisms, you can most easily accomplish this by using a drag-and-drop operation to move the DLL that contains the classes into the Components folder underneath your package.

To add objects to a package using drag-and-drop, do the following:

+   1. Make sure that the Components folder is selected.
+   2. In Windows Explorer, drag the DLL file into the right pane of the MTS Explorer window. MTS will add all the objects described in the type library.

You can also add objects to a package without drag-and-drop.

To add classes to the package without a drag-and-drop operation, do the following:

+   1. Expand the package branch where you want to insert components. Right-click the Components folder, point to New on the shortcut menu, and then select Component.
+   2. Click Install New Component(s) if you want to add every component in a certain DLL. This option is similar to using the drag-and-drop operation and does not require that the DLL be preregistered.