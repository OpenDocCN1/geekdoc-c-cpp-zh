![](bbox=[0.15, 0.12, 0.65, 0.48])

FIGURE 19-5

For custom event logging, you can use classes from the `System.Diagnostics` namespace.

# Event-Logging Architecture

The event log information is stored in several log files. The most important ones are application, security, and system. Looking at the registry configuration of the event log service, you will notice several entries under HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\EventLog with configurations pointing to the specific files. The system log file is used from the system and device drivers. Applications and services write to the application log. The security log is a read-only log for applications. The auditing feature of the operating system uses the security log. Every application can also create a custom category and log file to write event log entries there. For example, this is done by Media Center.

You can read these events by using the administrative tool Event Viewer. The Event Viewer can be started directly from the Server Explorer of Visual Studio by right-clicking the Event Logs item and selecting the Launch Event Viewer entry from the context menu. The Event Viewer is shown in Figure 19-6.

![](bbox=[0.12, 0.7, 0.7, 0.95])

FIGURE 19-6