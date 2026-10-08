# 466 Using the System.Net Namespace

```
<add name="FileLog"
type="Microsoft.VisualBasic.Logging.FileLogTraceListener"
Microsoft.VisualBasic, Version=8.0.0.0, Culture=neutral, PublicKeyToken=b03f
5f7f1d50a3, processorArchitecture=MSIL
initializeData="FileLogWriter" />
<!-- Uncomment the below section and replace APPLICATION_NAME with
the name of your application to write to the Event Log -->
<!--<add name="EventLog" type="System.Diagnostics.EventLogTraceListener"
  initializeData="APPLICATION_NAME" />
</sharedListeners>
</system.diagnostics>
```

First, you need to add a new source for the System.Net namespace. Next, you add a switch to the Switches source for the source you added. Finally, you add a SharedListener to that section and set the file for tracing information automatically.

The finished app.config file, with the adds in bold, is shown in Listing 4-4. It's also in the sample code on this book's Web site.

# Listing 4-4: The finished app.config File

```
<xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.diagnostics>
    <source name="Microsoft.VisualBasic.Logging.Log.WindowsFormsSource"
      switchName="DefaultSwitch">
      <listeners>
        <add name="FileLog" />
      </listeners>
    </source>
    <source name="System.Net">
      <listeners>
        <add name="System.Net" />
      </listeners>
    </source>
    <switches>
      <add name="DefaultSwitch" value="Information" />
      <add name="System.Net" value="Verbose" />
    </switches>
    <sharedListeners>
      <add name="FileLog"\n        type="Microsoft.VisualBasic.Logging.FileLogTraceListener"
        Microsoft.VisualBasic, Version=8.0.0.0, Culture=neutral, PublicKeyToken=b03f
5f7f1d50a3, processorArchitecture=MSIL
        initializeData="FileLogWriter" />
      <add name="System.Net"
        type="System.Diagnostics.TextWriterTraceListener"
        initializeData="my.log" />
    </sharedListeners>
    <trace autoflush="true" />
  </system.diagnostics>
</configuration>
```