```
```csharp
var evLog = new EventLog(logName, "*", sourceName);
evLog.RegisterDisplayName(resourceFile, 5001);
```
```

Now, you can use the WriteEvent() method instead of WriteEntry() to write the event log entry. WriteEvent() requires an object of type EventInstance as parameter. With the EventInstance, you can assign the message ID, the category, and the severity of type EventLogEntryType. In addition to the EventInstance parameter, WriteEvent() accepts parameters for messages that have parameters and binary data in the form of a byte array.

```
```csharp
using (var log = new EventLog(logName, "*", sourceName))
{
    var info1 = new EventInstance(1000, 4,
        EventLogEntryType.Information);
    log.WriteEvent(info1);
    var info2 = new EventInstance(1001, 4,
        EventLogEntryType.Error);
    log.WriteEvent(info2, "avalon");
    var info3 = new EventInstance(1002, 3,
        EventLogEntryType.Error);
    byte[] additionalInfo = { 1, 2, 3 };
    log.WriteEvent(info3, additionalInfo);
}
```
```

> > For the message identifiers, it is useful to define a class with const values that provide a more meaningful name for the identifiers in the application.

You can read the event log entries with the Event Viewer.

# PERFORMANCE MONITORING

Performance monitoring can be used to get information about the normal behavior of applications. Performance monitoring is a great tool that helps you understand the workload of the system and observe changes and trends, particularly in applications running on the server.

Microsoft Windows has many performance objects, such as System, Memory, Objects, Process, Processor, Thread, Cache, and so on. Each of these objects has many counts to monitor. For example, with the Process object, the user time, handle count, page faults, thread count, and so on can be monitored for all processes or for specific process instances. Some applications, such as SQL Server, also add application-specific objects.

# Performance-Monitoring Classes

The System.Diagnostics namespace provides these classes for performance monitoring:

+   - PerformanceCounter can be used both to monitor counts and to write counts. New performance categories can also be created with this class.
+   - PerformanceCounterCategory enables you to step through all existing categories, as well as create new ones. You can programmatically get all the counters in a category.
+   - PerformanceCounterInstaller is used for the installation of performance counters. Its use is similar to that of the EventLogInstaller discussed previously.