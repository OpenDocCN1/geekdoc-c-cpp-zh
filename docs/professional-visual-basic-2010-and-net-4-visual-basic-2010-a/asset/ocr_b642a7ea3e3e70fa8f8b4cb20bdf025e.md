That’s it for the component’s code. To enable queuing, click Show All Files on the Solution Explorer to see the hidden files for the project. Expand the My Project item and then open the AssemblyInfo.vb file. Ensure that it has these attributes:

```
'Enterprise Services attributes
<Assembly: EnterpriseServices.ApplicationAccessControl(False,
    Authentication:=EnterpriseServices.AuthenticationOption.None)>
<Assembly: EnterpriseServices.ApplicationQueuing(Enabled:=True,
    QueueListenerEnabled:=True)>
<Assembly: EnterpriseServices.ApplicationName("WroxQueue")>
```

Code snippet from Queues

Next, ensure that queuing is correctly enabled for this component. The next line is a special line to enable message queuing to work correctly in a workgroup environment, by switching off authentication. If you didn’t do this, you would need to set up an entire domain structure and create specific users for the queues. (In a production scenario, that’s exactly what you would use, so you would need to remove this line.) Finally, ensure that the component runs as a server, rather than a library. This was optional for transactional components, but it’s mandatory for queued components. You’ll soon see why. In addition, add a strong name file to your project, as you did with the Transactions component.

# Consoles Again

It’s time to build your Queues component. Once built, register it using RegSvcs just as you did with the Transactions component. Take a look at the Component Services Console to see how it’s going. Also, look closely at Figure D-15. It looks fine, but there’s one other console to check out: the Computer Management Console. Access this either from the system console or by right-clicking the My Computer icon and selecting Manage from the menu. Tucked away at the bottom is the relevant part. Open Services and Applications to find it. Component Services has set up some queues for us. There are five queues feeding into the main one, so the infrastructure is ready. Keep in mind that all this would be running on the server machine in a production scenario, not the client.

![](bbox=[0.09, 0.55, 0.72, 0.895])

FIGURE D-15