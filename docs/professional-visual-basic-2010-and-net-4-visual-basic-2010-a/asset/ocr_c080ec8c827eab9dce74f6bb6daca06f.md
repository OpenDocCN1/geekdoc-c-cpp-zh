The Transactions section allows for the use of WS-Coordination and WS-AtomicTransaction. WS-Coordination is there for the purpose of addressing the description of the relationships that multiple services have to one another. As a company starts developing a multitude of services within its enterprise, it realizes that many of the services developed have a relationship with one another, and that’s where WS-Coordination comes into play. This specification is meant to be expanded by other specifications that will further define particular coordination types.

WS-AtomicTransaction uses WS-Coordination and WS-Security to allow for the definition of a service transaction process. An atomic transaction is a way of creating a transaction process that works on an all-or-nothing basis. These are meant to be short-lived transactions, so when you use them you are locking data resources and holding onto physical resources such as connections, threads, and memory.

The main point of this discussion is to emphasize the slew of WS-* specifications at your disposal. Even better, when working with WCF you really don’t have to be aware that these specifications are even there — you can access the capabilities these specifications offer through programmatic or declarative programming.

# BUILDING A WCF SERVICE

Building a WCF service is not hard to accomplish. Using Visual Studio 2010, you’ll see the WCF new project templates shown in Figure 13-2. One word of warning however, in order to host a WCF service you’ll need to have started Visual Studio with the Run as Administrator menu link. Before attempting to replicate all of the steps in the sample, make sure you’ve started Visual Studio using the ‘Run as Administrator’ option from the context menu.

![](bbox=[0.09, 0.46, 0.75, 0.78])

FIGURE 13-2

When you build a WCF project in this manner, the idea is that you build a traditional Class Library that is compiled down to a DLL that can then be added to another project. The separation of code and use of multiple projects is a powerful tool for managing complexity on larger projects. That said, though, you can also just as easily build a WCF service directly in your .NET project, whether that is a console application or a Windows Forms application.

This example will first create a new WCF service in a Service Library. It then demonstrates how to host the WCF service inside a console application. Start by creating a new Service Library with the name ProVB_WCFCalculatorService.