4. Enter the name of the endpoint as HttpBinding, address as http://localhost:1982/MyFirstWCFService/Service.svc, binding as customBinding, binding configuration as NetHttpBinding, and contract as IService, in the respective fields, as shown in Figure 19.17:

![](bbox=[0.26, 0.125, 0.785, 0.355])

An endpoint is added in the Endpoints node of Microsoft Service Configuration Editor.

> NOTE
> You can also specify multiple endpoints for your service.

Now, let’s discuss about specifying the service behavior.

# Specifying the Service Behavior

Perform the following steps to specify the service behavior in the configuration file of your WCF service:

+   1. Expand the Advanced folder in the Configuration pane.
+   2. Right-click the Service Behaviors folder and select the New Service Behavior Configuration option from the context menu.
+   3. Change the name of the service behavior to MyServiceBehavior in the Service Behaviors node.
+   4. Add serviceMetadata, serviceDebug, and serviceThrottling in the Behavior element extension position section, as shown in Figure 19.18:

![](bbox=[0.255, 0.63, 0.785, 0.9])