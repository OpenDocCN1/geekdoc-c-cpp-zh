+   - The `ServiceController` class is used to implement a service control program. With this class, you can send requests to services.
+   - The `ServiceProcessInstaller` and `ServiceInstaller` classes are, as their names suggest, classes to install and configure service programs.

Now you are ready to create a new service.

# Creating a Windows Service Program

The service that you create in this chapter hosts a quote server. With every request that is made from a client, the quote server returns a random quote from a quote file. The first part of the solution uses three assemblies: one for the client and two for the server. Figure 39.4 provides an overview of the solution. The assembly `QuoteServer` holds the actual functionality. The service reads the quote file in a memory cache and answers requests for quotes with the help of a socket server. The `QuoteClient` is a WPF rich–client application. This application creates a client socket to communicate with the `QuoteServer`. The third assembly is the actual service. The `QuoteService` starts and stops the `QuoteServer`; the service controls the server.

![](bbox=[0.105, 0.447, 0.895, 0.67])

Figure 39.4

Before creating the service part of your program, create a simple socket server in an extra C# class library that will be used from your service process. How this can be done is discussed in the following section.

# Creating Core Functionality for the Service

You can build any functionality in a Windows Service, such as scanning for files to do a backup or a virus check or starting a WCF server. However, all service programs share some similarities. The program must be able to start (and to return to the caller), stop, and suspend. This section looks at such an implementation using a socket server.

With Windows 10, the Simple TCP/IP Services can be installed as part