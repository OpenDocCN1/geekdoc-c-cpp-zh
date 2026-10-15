```
minRequiredNonAlphanumericCharacters="0" passwordAttemptWindow="10" applicationName="/"/>
</providers>
</membership>
<profile>
  <providers>
    <clear/>
    <add name="AspNetSqlProfileProvider"
         type="System.Web.Profile.SqlProfileProvider"
         connectionStringName="ApplicationServices" applicationName="/"/>
  </providers>
</profile>
<roleManager enabled="false">
  <providers>
    <clear/>
    <add name="AspNetSqlRoleProvider"
         type="System.Web.Security.SqlRoleProvider"
         connectionStringName="ApplicationServices" applicationName="/"/>
    <add name="AspNetWindowsTokenRoleProvider"
         type="System.Web.Security.WindowsTokenRoleProvider"
         applicationName="/"/>
  </providers>
</roleManager>
</system.web>
<system.webServer>
  <modules runAllManagedModulesForAllRequests="true"/>
</system.webServer>
<system.serviceModel>
  <behaviors>
    <serviceBehaviors>
      <behavior name="MyServiceTypeBehaviors">
        <serviceMetadata httpGetEnabled="true"/>
      </behavior>
    </serviceBehaviors>
    <endpointBehaviors>
      <behavior name="OperationServiceAspNetAjaxBehavior">
        <enableWebScript/>
      </behavior>
    </endpointBehaviors>
  </behaviors>
  <serviceHostingEnvironment aspNetCompatibilityEnabled="true" multipleSiteBindingsEnabled="true"/>
  <services>
    <service name="OperationService" behaviorConfiguration="MyServiceTypeBehaviors">
      <endpoint address="" behaviorConfiguration="OperationServiceAspNetAjaxBehavior" binding="webHttpBinding" contract="OperationService"/>
      <endpoint contract="IMetadataExchange" binding="mexHttpBinding" address="mex"/>
    </service>
  </services>
</system.serviceModel>
</configuration>
```

5. Run the OperationService service. When you run the OperationService service, you get a message, You have created a service, as shown in Figure 19.44;