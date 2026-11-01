```
Language=English
Connection successful.
.
MessageId = 1001
Severity = Error
Facility = Application
SymbolicName= MSG_CONNECT_FAILED_1001
Language=English
Could not connect to server %1.
.
MessageId = 1002
Severity = Error
Facility = Application
SymbolicName= MSG_DB_UPDATE_1002
Language=English
Database update failed.
.
MessageId = 1003
Severity = Success
Facility = Application
SymbolicName= APP_UPDATE
Language=English
Application %S002 updated.
.
; // - Event log display name -
; // ****************************************
MessageId = 5001
Severity = Success
Facility = Application
SymbolicName= EVENT_LOG_DISPLAY_NAME_MSGID
Language=English
Professional C# Sample Event Log
.
; // - Event message parameters -
; //      Language independent insertion strings
; // ****************************************
MessageId = 5002
Severity = Success
Facility = Application
SymbolicName= EVENT_LOG_SERVICE_NAME_MSGID
Language=English
EventLogDemo.EXE
.
```

code snippet EventLogDemo/EventLogDemoMessages.mc

Use the Messages Compiler, mc.exe, to create a binary message file. The command mc -s EventLogDemoMessages.mc compiles the source file containing the messages to a messages file with the .bin extension and the file Messages.rc, which contains a reference to the binary message file:

```
mc -s EventLogDemoMessages.mc
```