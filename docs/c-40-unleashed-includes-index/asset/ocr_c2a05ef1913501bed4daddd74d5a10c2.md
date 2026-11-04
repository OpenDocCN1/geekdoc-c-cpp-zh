+   - **Event logs** are useful from a management perspective both for inspection and the emission of diagnostic information during execution of the program. .NET has rich support to deal with logging infrastructure.
+   - **Management Classes and Events** are two faces for the **Windows Management Instrumentation** (WMI) technology, allowing for thorough querying and modification of the system's configuration.
+   - **Message queues** enable reliable, possibly offline, communication between machines using the Microsoft Message Queuing (MSMQ) technology. To send and receive data to and from a queue, a mapping object can be made.
+   - **Performance counters** are another cornerstone of application manageability, providing the capability to emit diagnostic performance information to counters in the system (for example, the number of requests served per second by a service).
+   - The Services node provides a gateway to management of **Windows Services**, such as querying of installed services, their states, and configuration and to control them. In fact, C# can even be used to write managed code OS services.

For example, in Figure 3.55, a component designer was used to create a management component containing management objects for a Windows server, a performance counter, and an event log. No code had to be written manually thanks to the drag-and-drop support from the Server Explorer onto the designer surface. The Properties window can be used to tweak settings for the generated objects.

![](bbox=[0.07, 0.71, 0.78, 0.9])

FIGURE 3.55 Component designer surface with management objects.