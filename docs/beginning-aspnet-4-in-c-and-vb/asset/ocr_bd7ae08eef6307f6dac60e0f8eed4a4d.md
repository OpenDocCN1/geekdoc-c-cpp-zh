An application manifest is an XML file similar to the application configuration file. While the application configuration file has the file extension .config, the manifest ends with .manifest. The name of the file must be set to the name of the application, including the .exe file extension followed by .manifest. Visual Studio renames and copies the app.manifest file just as it does an application configuration file. The manifest file contains XML data, as shown here. The root element is <assembly>, which contains the child element <trustInfo>. The administrator requirement is defined with the level attribute of the <requestedExecutionLevel> element.

```
<?xml version="1.0" encoding="utf-8"?>
<asmv1:assembly manifestVersion="1.0" xmlns="urn:schemas-microsoft-com:asm.v1" xmlns:asmv2="urn:schemas-microsoft-com:asm.v2" xmlns:asmv3="urn:schemas-microsoft-com:asm.v3" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <assemblyIdentity version="1.0.0.0" name="MyApplication.app"/>
  <trustInfo xmlns="urn:schemas-microsoft-com:asm.v2">
    <security>
      <requestedPrivileges xmlns="urn:schemas-microsoft-com:asm.v3">
        <requestedExecutionLevel level="requireAdministrator" uiAccess="false" />
      </requestedPrivileges>
    </security>
  </trustInfo>
</asmv1:assembly>
```

*code snippet AdminRightsRequired\app.manifest*

When starting the application this way, you get an elevation prompt where the user is asked if he or she trusts the application to run with administrative privileges.

With the requestedExecutionLevel setting, you can specify the values requireAdministrator, highestAvailable, and asInvoker. The value highestAvailable means that the application gets the privileges the user has — but only after getting the consent from the user. The value requireAdministrator requires Administrator privileges. If the user is not logged on to the system as Administrator, a login dialog appears where the user can log in as Administrator for the application. The value asInvoker means that the application is running with the security token of the user.

The uiAccess attribute specifies if the application requires input to a higher-privilege-level window on the desktop. For example, an onscreen keyboard needs to drive input to other windows on the desktop, so the setting should be set to true for the application to display the onscreen keyboard. Non-UI-accessible applications should have this attribute set to false.

![](bbox=[0.15, 0.72, 0.85, 0.85])

# Shield Icon

If an application or a task from an application requires administrative privileges, the user is informed by an easily recognizable shield icon. The shield icon is attached to the controls that require elevation. The user expects to see an elevation prompt when clicking on an item with a shield. Figures A-5 and A-6 show the shield in use. The Task Manager requires elevation to see processes from all users. Within User Accounts, adding or removing user accounts requires elevation as well as setting up parental controls.