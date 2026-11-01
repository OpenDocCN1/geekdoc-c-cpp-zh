To create services using an application configuration file, you need to add a section handler for the workflow runtime and then add services to this section as shown here:

```
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <section name="WF"
      type="System.Workflow.Runtime.Configuration.WorkflowRuntimeSection,
      System.Workflow.Runtime, Version=3.0.00000.0, Culture=neutral,
      PublicKeyToken=31bf3856ad364e35" />
  </configSections>

  <WF Name="Hosting">
    <CommonParameters/>
    <Services>
      <add type="System.Workflow.Runtime.Hosting.SqlWorkflowPersistenceService,
        System.Workflow.Runtime, Version=3.0.00000.0, Culture=neutral,
        PublicKeyToken=31bf3856ad364e35"
        connectionString="Initial Catalog=WF;Data Source=.;
        Integrated Security=SSPI;"
        UnloadOnIdle="true"
        LoadIntervalSeconds="2"/>
      <add type="System.Workflow.Runtime.Tracking.SqlTrackingService,
        System.Workflow.Runtime, Version=3.0.00000.0, Culture=neutral,
        PublicKeyToken=31bf3856ad364e35"
        connectionString="Initial Catalog=WF;Data Source=.;
        Integrated Security=SSPI;"
        UseDefaultProfile="true"/>
    </Services>
  </WF>
</configuration>
```

Within the configuration file, you have added the WF section handler (the name is unimportant but must match the name given to the later configuration section) and then created the appropriate entries for this section. The <Services> element can contain an arbitrary list of entries that consist of a .NET type and then parameters that will be passed to that service when constructed by the runtime.

To read the configuration settings from the application configuration file, you call another constructor on the runtime, as shown here:

```
using(WorkflowRuntime workflowRuntime = new WorkflowRuntime("WF"))
{
  .
}
```

This constructor will instantiate each service defined within the configuration file and add these to the services collection on the runtime.

The following sections describe some of the standard services available with WF.

# The Persistence Service

When a workflow executes, it may reach a wait state. This can occur when a delay activity executes or when you are waiting for external input within a ListenActivity. At this point, the workflow is said to be idle and as such is a candidate for persistence.

Let's assume that you begin execution of 1,000 workflows on your server, and each of these instances becomes idle. At this point, it is unnecessary to maintain data for each of these instances in memory, so it would be ideal if you could unload a workflow and free up the resources in use. The persistence service is designed to accomplish this.

When a workflow becomes idle, the workflow runtime checks for the existence of a service that derives from the WorkflowPersistenceService class. If this service exists, it is passed the workflow instance, and the