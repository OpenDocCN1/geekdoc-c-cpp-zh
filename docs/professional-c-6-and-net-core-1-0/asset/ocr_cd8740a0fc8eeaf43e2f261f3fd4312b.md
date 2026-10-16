```
<template tid="ServiceErrorArgs">
    <data name="message" inType="win:UnicodeString"/>
    <data name="error" inType="win:Int32"/>
</template>
</templates>
</provider>
</events>
</instrumentation>
<localization>
    <resources culture="en-GB">
        <stringTable>
            <string id="FileName_event_CalledService" value="%1 length: %2"/>
            <string id="FileName_event_CallService" value="%1"/>
            <string id="FileName_event_ServiceError" value="%1 error: %2"/>
            <string id="FileName_keyword_Database" value="Database"/>
            <string id="FileName_keyword_Diagnostics" value="Diagnostics"/>
            <string id="FileName_keyword_Network" value="Network"/>
            <string id="FileName_keyword_Performance" value="Performance"/>
            <string id="FileName_keyword_Session0" value="Session0"/>
            <string id="FileName_keyword_Session1" value="Session1"/>
            <string id="FileName_keyword_Session2" value="Session2"/>
            <string id="FileName_keyword_Session3" value="Session3"/>
            <string id="FileName_task_CreateMenus" value="CreateMenus"/>
            <string id="FileName_task_EventSourceMessage" value="EventSourceMessage"/>
            <string id="FileName_task_QueryMenus" value="QueryMenus"/>
        </stringTable>
    </resources>
</localization>
</instrumentationManifest>
```

Having this metadata and registering it with the system allows the system administrator to filter for specific events and get notifications when something happens. You can handle registration in two ways: static and dynamic. Static registration requires administrative privileges, and a registration via the wevtutil.exe command-line tool, which passes the DLL that contains the manifest. The EventSource class also offers the preferred dynamic registration. This happens during runtime without the need for administrative privileges returning the manifest in an event stream, or in a response to a standard ETW command.

# Using Activity IDs

A new feature of the new version of TraceSource makes it possible to easily write activity IDs. As soon as you have multiple tasks running, it helps to know which trace messages belong to each other and not have the trace message based only on time. For example, when you’re using