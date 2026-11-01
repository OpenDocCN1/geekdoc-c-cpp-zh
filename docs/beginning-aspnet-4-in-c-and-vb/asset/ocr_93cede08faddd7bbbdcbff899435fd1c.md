Here are a few examples of services:

+   - Simple TCP/IP Services is a service program that hosts some small TCP/IP servers: echo, daytime, quote, and others.
+   - World Wide Web Publishing Service is the service of the Internet Information Server (IIS).
+   - Event Log is a service to log messages to the event log system.
+   - Windows Search is a service that creates indexes of data on the disk.

You can use the Services administration tool, shown in Figure 25-1, to see all the services on a system. This program can be found with the Administrative Tools.

![](bbox=[0.1, 0.37, 0.8, 0.67])

FIGURE 25-1

# WINDOWS SERVICES ARCHITECTURE

Three program types are necessary to operate a Windows Service:

+   - A service program
+   - A service control program
+   - A service configuration program

The service program itself provides the actual functionality you are looking for. With a service control program, it is possible to send control requests to a service, such as start, stop, pause, and continue. With a service configuration program, a service can be installed; it is copied to the file system, written into the registry, and configured as a service. Although .NET components can be installed simply with an xcopy — because they don't need to write information to the registry — installation for services requires registry configuration. A service configuration program can also be used to change the configuration of that service at a later point.

These three ingredients of a Windows Service are discussed in the following subsections.

# Service Program

Before looking at the .NET implementation of a service, let's explore, from an independent point of view, what the Windows architecture of services looks like and what the inner functionality of a service is.