# DEFINING YOUR APPLICATION UAC SETTINGS

By default in Visual Studio 2010, your application settings include information related to UAC. It is possible to create your application so that it ships with certain permissions. Within your application manifest you'll find the section requestedPrivileges. This section is where the requested UAC execution level for your application is defined.

To get to your application manifest, right-click on your project in Solution Explorer and select Properties. In the Properties pane, select the Application tab and there you'll find a button labeled View Windows Settings. Selecting this button will open your application manifest (app.manifest) XML file in the editor window. Within the XML, you'll find the requestedPrivileges node, a copy of which is shown in the following code block:

```
<requestedPrivileges xmlns="urn:schemas-microsoft-com:asm.v3">
    <!-- UAC Manifest Options
        If you want to change the Windows User Account Control level replace the
        requestedExecutionLevel node with one of the following.

        <requestedExecutionLevel level="asInvoker" uiAccess="false" />
        <requestedExecutionLevel level="requireAdministrator" uiAccess="false" />
        <requestedExecutionLevel level="highestAvailable" uiAccess="false" />

        Specifying requestedExecutionLevel node will disable file and registry
        virtualization. If you want to utilize File and Registry Virtualization
        for backward compatibility then delete the requestedExecutionLevel node.-->
    <requestedExecutionLevel level="asInvoker" uiAccess="false" />
</requestedPrivileges>
```

Code snippet from app.manifest

The beauty of this XML is that Microsoft took the time to include meaningful XML comments about the requestedExecutionLevel setting. By default, as shown in the preceding snippet, your application requests to run asInvoker. Thus, as discussed earlier when looking at which group you are running as, this means you are running as a user, not an administrator.

As the comments make clear, it is possible to change this to requireAdministrator, so make this change. Next ensure that you have both the Sub DisplayPrincipalIdentity() and the Sub TestFileIOPermission() uncommented in the ButtonTest click event handler within the ProVB_Security project. Finally, within the Sub TestFileIOPermission(), ensure that you have restored which block is commented out; the code should look like the previous listing where the bottom half of the method is commented and the top half is uncommented. Now that you have indicated that this application requires administrator privileges, you can repeat the first test where the user account didn't have permission to write to NoPermission.txt, but where the code attempted to grant permission. Note, this test depends on the Administrator having permission to access the file C:\Test\NoPermission.txt. Save your change to the app.manifest and attempt to run the application. If you are running on Windows 7 and didn't start Visual Studio 2010 using Run as Administrator you should get the error shown in Figure 32-6.

![](bbox=[0.13, 0.73, 0.66, 0.91])

FIGURE 32-6