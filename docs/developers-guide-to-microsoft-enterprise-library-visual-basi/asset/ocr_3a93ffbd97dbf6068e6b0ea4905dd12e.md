Then, all you need to do is load this configuration into a new Unity container. This requires just one line of code, as shown here.

```
Dim theContainer = New UnityContainer().LoadConfiguration()
```

> Other techniques we demonstrate in Appendix A, “Dependency Injection with Unity,” include using attributes to register type mappings and dependencies, defining named registrations, and specifying dependencies and values for parameters and properties

The one point to be aware of when you use the more sophisticated technique for creating objects is that your application is responsible for managing the container, holding a reference to it, and making that reference available to code that must access the container. In forms-based applications that automatically maintain global state (for example, applications built using technologies such as Windows Forms, Windows Presentation Foundation (WPF), and Silverlight®), you can use an application-wide variable for this.

However, in request-based applications built using technologies such as ASP.NET, ASMX, and Windows Communication Foundation (WCF), you generally require additional code to maintain the container and make it available for each request. We discuss some of the ways that you can achieve this in Appendix B, “Dependency Injection in Enterprise Library,” and you will find full details in the documentation installed with Enterprise Library and available online at http://go.microsoft.com/fwlink/?LinkId=188874.

# GETTING OBJECTS FROM PREVIOUS VERSIONS OF ENTERPRISE LIBRARY

If you have used versions of Enterprise Library prior to version 5.0, you may be more familiar with the previous approach to creating objects within your application code. Earlier versions generally supported or recommended the use of a series of static facades. While these facades are still supported in version 5.0 for backward compatibility with existing applications, they are no longer the recommended approach and may be deprecated in future releases.

Figure 5 summarizes all the approaches you can use to get access to the features of Enterprise Library. 1 and 2 are the recommended approaches for Enterprise Library 5.0; 3 and 4 are still supported to make it easier to upgrade your existing applications that use a previous version of Enterprise Library.