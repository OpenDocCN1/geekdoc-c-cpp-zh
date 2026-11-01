this configuration is such that you can apply pretty much any configuration that you can think of to a service, and you can even extend this syntax.

WCF configuration code is contained in the <system.serviceModel> configuration section of Web.config or app.config files. In this example, there is not a lot of service configuration, as default values are used. In the Web.config file, the configuration section consists of a single subsection that supplies overrides to default values for the service behavior <behaviors>. The code for the <system.serviceModel> configuration section in Web.config (with comments removed for clarity) is as follows:

```
<system.serviceModel>
  <behaviors>
    <serviceBehaviors>
      <behavior>
        <serviceMetadata httpGetEnabled="true" httpsGetEnabled="true" />
        <serviceDebug includeExceptionDetailInFaults="false" />
      </behavior>
    </serviceBehaviors>
  </behaviors>
</system.serviceModel>
```

This section can define one or more behaviors in <behavior> child sections, which can be reused on multiple other elements. A <behavior> section can be given a name to facilitate this reuse (so that it can be referenced from elsewhere), or can be used without a name (as in this example) to specify overrides to default behavior settings.

> NOTE If nondefault configuration were being used, you would expect to see a <services> section inside <system.serviceModel>, containing one or more <services> child sections. In turn, the <service> sections can contain child <endpoint> sections, each of which (you guessed it) defines an endpoint for the service. In fact, the endpoints defined are base endpoints for the service. Endpoints for operations are inferred from these.

One of the default behavior overrides in Web.config is as follows:

```
<serviceDebug includeExceptionDetailInFaults="false"/>
```

This setting can be set to true to expose exception details in any faults that are transmitted to the client, which is something you would usually allow only in development.