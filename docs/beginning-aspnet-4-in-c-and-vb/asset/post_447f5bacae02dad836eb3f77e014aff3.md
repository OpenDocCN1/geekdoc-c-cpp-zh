
```
textStatus.Text += String.Format("{0:T}: Registered for recovery\n", DateTime.Now);
App.Source.TraceEvent(TraceEventType.Verbose, 0, "Registered for recovery");
}
```

DoRecovery() is the callback method that is defined by the RegisterForApplicationRecovery() method call and is invoked by WER. Within the handler, the Recovery Manager is informed that recovery is in progress by calling the method ApplicationRecoveryInProgress(). This method returns true if the user canceled the recovery. You can verify user cancellation during the recovery to stop the recovery in case it was canceled by the user. Here, the content of the TextBox is written to the temporary file that is used when restarting the application. At the end of the recovery process, the Restart Manager is informed of its success by invoking ApplicationRecoveryFinished().

```
private int DoRecovery(object state)
{
    App.Source.TraceEvent(TraceEventType.Verbose, 0, "begin Recovery");
    this.tempPath = (string)state;
    bool canceled = ApplicationRestartRecoveryManager.
        ApplicationRecoveryInProgress();
    if (canceled)
    {
        textStatus.Text += String.Format
            ("{0:T}: Recovery canceled, shutting down\n", DateTime.Now);
        App.Source.TraceEvent(TraceEventType.Verbose, 0,
            "end Recovery with cancel");
        ApplicationRestartRecoveryManager.ApplicationRecoveryFinished(
            false);
        return 0;
    }
    SaveFile(tempPath);
    App.Source.TraceEvent(TraceEventType.Verbose, 0, "end Recovery");
    ApplicationRestartRecoveryManager.ApplicationRecoveryFinished(true);
    return 0;
}
```

With all this in place, you can run the application, as shown in Figure A-2. The TextBlock on the bottom gives status information such as when registering for restart and recovery happened, and after 60 seconds, information that the application can now crash.

![](img/d7d2ffa0a76feaab821930e95daace93_1464_0.png)

FIGURE A-2

Selecting the menu Action ▸ Crash invokes the handler method OnCrash(), which does a fast fail. The method Environment.FailFast() can be used to terminate a process in a fast way. This method writes an application event log and creates a dump of the application before the process is terminated. Only CriticalFinalizerObject objects are executed. Try-finally blocks and finalizers are not executed.

```
private void OnCrash(object sender, ExecutedRoutedEventArgs e)
{
    Environment.FailFast("RestartDemo stopped from Menu command");
}
```

After crashing, the application is restarted and you can see the dialog shown in Figure A-3.

![](img/d7d2ffa0a76feaab821930e95daace93_1464_1.png)

FIGURE A-3

## USER ACCOUNT CONTROL

As a developer, user account control (UAC) is one of the features you can see immediately with Windows Vista: every time an administrative task is done, a dialog pops up asking for admin rights. In Windows 7, you can now configure this feature, as shown in Figure A-4. The default setting is to provide no notifications if admin changes are required from applications that are part of the operating system.

![](img/d7d2ffa0a76feaab821930e95daace93_1465_0.png)

FIGURE A-4

What's the purpose behind the hassle of these dialogs? Although Windows guidelines have always mentioned that applications should not require admin privileges if it's not really necessary, many applications still need to run with the administrator account. For example, a normal user is not allowed to write data to the program files directory; administrative privileges are required. Because many applications don't run without administrative privileges as the developers didn't follow the guidelines, many users log in to the system with an Administrator account. By using the Administrator account on daily work you can unintentionally install Trojan horse programs.

Windows Vista and later versions avoid this problem because the Administrator, by default, doesn't have administrative privileges. The process has two security tokens associated with it, one with normal user privileges and one with admin privileges (for the case where the login is done to the Administrator account). With applications that require administrative privileges, the user can elevate the application to run with Administrator rights. This can either be done from the context menu Run as Administrator option, or the Compatibility Properties of an application can be configured to always require administrator privileges to run it. This setting adds application compatibility flags to the registry at `HKCU\Software\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\Layers` with a value for `RUNASADMIN`.

### Applications Requiring Admin Privileges

For applications that require administrative privileges, you can also add an application manifest. Visual Studio 2010 has an item template to add an application manifest to an application. Such a manifest can be created either by adding a manifest file to an existing application or by embedding a Win32 resource file within the assembly. In the Application tab of the Project Properties, you can select the manifest file of the application that's included as a native resource.

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

![](img/d7d2ffa0a76feaab821930e95daace93_1466_0.png)

### Shield Icon

If an application or a task from an application requires administrative privileges, the user is informed by an easily recognizable shield icon. The shield icon is attached to the controls that require elevation. The user expects to see an elevation prompt when clicking on an item with a shield. Figures A-5 and A-6 show the shield in use. The Task Manager requires elevation to see processes from all users. Within User Accounts, adding or removing user accounts requires elevation as well as setting up parental controls.
