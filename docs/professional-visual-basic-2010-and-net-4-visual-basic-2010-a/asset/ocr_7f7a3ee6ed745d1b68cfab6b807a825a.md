```
<section name="ProVB_VS2010.My.MySettings" type="System.Configuration.ClientSettingsSection, System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" allowExeDefinition="MachineToLocalUser" requirePermission="false" />
    <sectionGroup>
        <sectionGroup name="applicationSettings" type="System.Configuration.ApplicationSettingsGroup, System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" >
            <section name="ProVB_VS2010.My.MySettings" type="System.Configuration.ClientSettingsSection, System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
        </sectionGroup>
    </sectionGroup>
</configSections>
<system.diagnostics>
    <sources>
        <!-- This section defines the logging configuration for My.Application.Log -->
        <source name="DefaultSource" switchName="DefaultSwitch">
            <listeners>
                <add name="FileLog"/>
                <!-- Uncomment the below section to write to the Application Event Log -->
                <!--add name="EventLog"/-->
            </listeners>
        </source>
    </sources>
    <switches>
        <add name="DefaultSwitch" value="Information" />
    </switches>
    <sharedListeners>
        <add name="FileLog" type="Microsoft.VisualBasic.Logging.FileLogTraceListener, Microsoft.VisualBasic, Version=8.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL" initializeData="FileLogWriter"/>
        <!-- Uncomment the below section and replace APPLICATION_NAME with the name of your application to write to the Application Event Log -->
        <!--add name="EventLog" type="System.Diagnostics.EventLogTraceListener" initializeData="APPLICATION_NAME"/-->
    </sharedListeners>
</system.diagnostics>
<userSettings>
    <ProVB_VS2010.My.MySettings>
        <setting name="LastLocation" serializeAs="String">
            <value>0, 0</value>
        </setting>
    </ProVB_VS2010.My.MySettings>
</userSettings>
<applicationSettings>
    <ProVB_VS2010.My.MySettings>
        <setting name="ConnectionString" serializeAs="String">
            <value>server=(local);Database=adventureworks</value>
        </setting>
    </ProVB_VS2010.My.MySettings>
</applicationSettings>
</configuration>
```

Code snippet from app.config

As shown here, Visual Studio automatically generated all the XML needed to define these settings and save the default values. Note that individual user settings are not saved back into the config file, but rather to a user-specific working directory. In fact, it is possible not only to update application settings with Visual Basic,