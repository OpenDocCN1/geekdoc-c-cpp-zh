# Table 20.1: Noteworthy Public Properties of the ServiceBase Class

| Property | Description |
|---|---|
| CanHandleSessionChangeEvent | Determines whether or not a Windows service can handle session change events returned by a Terminal Server session |
| CanPauseAndContinue | Determines whether or not you can pause and resume a Windows service |
| CanShutdown | Determines whether or not a Windows service should be notified when the system is shutting down |
| CanStop | Determines whether or not a Windows service can be stopped |
| EventLog | Obtains an event log that you can use to write to the Application event log |
| ExitCode | Determines the exit code for a Windows service |
| ServiceName | Specifies the name of a Windows service |

Table 20.2 describes some noteworthy public methods of the ServiceBase class:

# Table 20.2: Noteworthy Public Methods of the ServiceBase Class

| Method | Description |
|---|---|
| Dispose | Disposes off the resources used by the ServiceBase class |
| RequestAdditionalTime | Requests for additional time to complete a pending operation |
| Run | Registers the executable for a Windows service with SCM |
| ServiceMainCallback | Registers the command handler to Windows operating system and starts the corresponding Windows service |
| Stop | Stops the Windows service |

Let's now explore another class, ServiceInstaller.

# The ServiceInstaller Class

The ServiceInstaller class is used to install a Windows service application. This class is used to write the registry values associated with a Windows service to the HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services registry key. A Windows service is identified by the name assigned to the ServiceName property of the ServiceInstaller class. You can install a Windows service by creating a project installer class that inherits from the Installer class.

The inheritance hierarchy of the ServiceInstaller class is as follows:

```
System.Object
  System.MarshalByRefObject
    System.ComponentModel.Component
      System.Configuration.Install.Installer
        System.Configuration.Install.ComponentInstaller
          System.ServiceProcess.ServiceInstaller
```

Table 20.3 describes some noteworthy public properties of the ServiceInstaller class:

# Table 20.3: Noteworthy Public Properties of the ServiceInstaller Class

| Property | Description |
|---|---|
| Description | Specifies the description of a Windows service |
| DisplayName | Specifies the display name of a Windows service |
| ServiceName | Specifies the name used to identify a Windows service |
| ServicesDependedOn | Specifies the services that must be running in support of a main Windows service |