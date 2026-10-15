
class on which the service is based, while the ServiceName property changes the name of the service as known to the Service Control Manager.

- 4. Add an installer to the project. Go back to the design surface for FileWatcherService and right-click it. Select Add Installer. A new file called ProjectInstaller1.vb is created and added to the project. The ProjectInstaller1.vb file has two components added to its design surface: ServiceProcessInstaller1 and ServiceInstaller1.

- 5. On the ProjectInstaller.vb design surface, highlight the ServiceProcessInstaller1 control. In its Properties window, change the Account property to LocalSystem.

- 6. Highlight the ServiceInstaller1 control. In its Properties window, type in FileWatcherService as the value of the DisplayName property. (The ServiceName property will already have this value.)

- 7. Build the project by right-clicking on the solution and selecting Build from the menu. An EXE named FileWatcherService.exe will be created for the service.

At this point, you have a Windows Service that is compiled and ready to be installed, but it doesn’t do anything yet. The preceding steps are very similar for every Windows Service you would create; the main points that vary are the name and the type of account you choose to use. The next part, however, is specific to a particular Windows Service: creating the application logic to support the functionality you need in the Windows Service.

## Adding .NET Components to the Service

This example service will have the capability to watch a directory for file changes and log events to report its activity. Two .NET components will facilitate these capabilities: the FileSystemWatcher component and the EventLog component.

## The FileSystemWatcher Component

The FileSystemWatcher component is used to monitor a particular directory. The component implements Created, Changed, Deleted, and Renamed events, which are fired when files are placed in the directory, changed, deleted, or renamed, respectively.

The operation that takes place when one of these events is fired is determined by the application developer. Most often, logic is included to read and process the new or changed files. However, you are just going to write a message to a log file.

To implement the component in the project, drag and drop a FileSystemWatcher control from the Components tab of the Toolbox onto the design surface of FileWatcherService.vb. (Be sure not to drag the component onto ProjectInstaller.vb. If ProjectInstaller.vb is still the displayed design surface, you'll need to click on the tab for the FileWatcherService.vb design surface.) This control is automatically called FileSystemWatcher1.

## The EnableRaisingEvents Property

The FileSystemWatcher component should not generate any events until the service is initialized and ready to handle them. To prevent this, set the EnableRaisingEvents property of FileSystemWatcher1 to False. This prevents the component from firing any events. You will enable it during the OnStart event in the service. These events fired by the FileSystemWatcher component are controlled using the NotifyFilter property, discussed later.

## The Path Property

The path that you want to monitor is the TEMP directory on the C: drive, so set the Path property to C:\TEMP (be sure to confirm that there is a TEMP directory on your C: drive). Of course, this path can be changed to monitor any directory depending on your system, including any network or removable drives.

## The NotifyFilter Property

For this example, you only want to monitor when a file is freshly created or the last modified value of a file has changed. To do this, set the NotifyFilter property to FileName, LastWrite. Note that you can specify multiple changes to monitor by including a comma-separated list. Even though the property has a drop-down, you’ll need to type in the value to get both parts of it.

You could also watch for other changes such as attributes, security, size, and directory name changes as well, just by including those options as part of the NotifyFilter property.

## The Filter Property

The types of files that you will look for are text files, so set the Filter property to *.txt. Note that if you were going to watch for all file types, then the value of the Filter property would be set to *.* (which is the default).

## The IncludeSubdirectories Property

If you wanted to watch subdirectories, you would set the IncludeSubdirectories property to True. This example leaves it as False, which is the default value. Figure 30-2 shows how the properties should be set.

![](img/d99870e80390742f93963da7be0b2e61_990_0.png)

## Adding FileSystemWatcher Code to OnStart and OnStop

Now that some properties are set, let’s add some code to the OnStart event for FileWatcherService.vb. You want to start the FileSystemWatcher1 component so it will start triggering events when files are created or copied into the directory you are monitoring, so set the EnableRaisingEvents property to True:

```
Protected Overrides Sub OnStart(ByVal args() As String)
' Add code here to start your service. This method should set things
' in motion so your service can do its work.
' Start monitoring for files
FileSystemWatcher1.EnableRaisingEvents = True
End Sub
```

Code snippet from FileWatcherService

After the file monitoring properties are initialized, you are ready to start the monitoring. When the service stops, you need to stop the file monitoring process. Add the following code to the OnStop event:

```
Protected Overrides Sub OnStop()
' Add code here to perform any tear-down necessary to stop your service.
' Stop monitoring for files
FileSystemWatcher1.EnableRaisingEvents = False
End Sub
```

Code snippet from FileWatcherService

## The EventLog Component

Now you are ready to place an EventLog component in the service to facilitate the logging of events. Event logs are available under the Windows operating system, and were discussed in Chapter 6. As with many other system-level features, the use of Event Logs is simplified in .NET because a .NET Framework base class does most of the work for you.

Depending on your system’s configuration and installed software, there should be several Event Logs on the system. Normally, your applications should only write to the Application Log. A property of a log entry called Source identifies the application writing the message. This property does not have to share the same name as the executable of the application, but it is often given that name to make it easy to identify the source of the message.

You can look at the events in the Event Log by using the Event Viewer. Select Control Panel ➝ Administrative Tools ➝ Event Viewer on Windows 2000; Start ➝ All Programs ➝ Administrative Tools ➝ Event Viewer on Windows XP; and Start ➝ Control Panel ➝ System and Maintenance ➝ Administrative Tools ➝ Event Viewer on Windows Vista and Windows 7. The example uses the Event Viewer to ensure that the service is generating events.

It was mentioned earlier in the chapter that the AutoLog property of the ServiceBase class determines whether the service automatically writes events to the Application Log. The AutoLog property instructs the service to use the Application event log to report command failures, as well as information for OnStart, OnStop, OnPause, and OnContinue events on the service. What is actually logged to the event log is an entry indicating whether the service started successfully and stopped successfully, and any errors that might have occurred.

You can turn off event log reporting by setting the AutoLog property to False in the Properties window for the service, but leave it set to True for this example. That means some events will be logged automatically (without you including any code for them). If desired, you can add some code to the service to log additional events not covered by the AutoLog property.

Drag and drop an EventLog control from the Components tab of the Toolbox onto the designer surface of FileWatcherService.vb. This control is automatically called EventLog1.

Set the Log property for Eventlog1 to Application, and set the Source property to FileWatcherService.

## The Created Event

Next, you will place some logic in the Created event of the FileSystemWatcher component to log when a file has been created. This event fires when a file has been placed or created in the directory that you are monitoring. It fires because the information last modified on the file has changed.

Bring up FileSystemWatcher1.vb in the code editor. Select FileSystemWatcher1 from the left hand drop-down list and then select Created from the right hand drop-down list. The Created event will be added to your code. Add code to the Created event as follows:

```
Public Sub FileSystemWatcher1_Created(ByVal sender As Object, _
    ByVal e As System.IO.FileSystemEventArgs) _
    Handles FileSystemWatcher1.Created
    Dim sMessage As String
    sMessage = "File created in directory - file name is " + e.Name
    EventLog1.WriteEntry(sMessage)
End Sub
```

Code snippet from FileWatcherService

Notice that the event argument’s object (the object named “e” in the event parameters) includes a property called Name. This property holds the name of the file that generated the event.

At this point, you could add the other events for FileSystemWatcher (Changed, Deleted, Renamed) in a similar way and create corresponding log messages for those events. To keep the example simple, you will just use the Created event in this service.

Build the service again to compile the new functionality. You are now ready to install the service and test it.
