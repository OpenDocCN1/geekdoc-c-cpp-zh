
## 25
## Windows Services
## WHAT'S IN THIS CHAPTER?
- The architecture of a Windows Service
- Windows Services installation programs
- Windows Services control programs
- Troubleshooting Windows Services

Windows Services are programs that can be started automatically at boot time without the need for anyone to log on to the machine. The following section explains the architecture of Windows Services. The rest of the chapter shows you how to create, monitor, control, and troubleshoot your Windows Services.

## WHAT IS A WINDOWS SERVICE?

Windows Services are applications that can be automatically started when the operating system boots. These applications can run without having an interactive user logged on to the system and do some processing in the background.

For example, on a Windows Server, system networking services should be accessible from the client without a user logging on to the server. And on the client system, services allow you to get a new software version from the Internet or to do some file cleanup on the local disk.

You can configure a Windows Service to run from a specially configured user account or from the system user account — a user account that has even more privileges than that of the system administrator.

![](img/d7d2ffa0a76feaab821930e95daace93_728_0.png)

Here are a few examples of services:
- Simple TCP/IP Services is a service program that hosts some small TCP/IP servers: echo, daytime, quote, and others.
- World Wide Web Publishing Service is the service of the Internet Information Server (IIS).
- Event Log is a service to log messages to the event log system.
- Windows Search is a service that creates indexes of data on the disk.

You can use the Services administration tool, shown in Figure 25-1, to see all the services on a system. This program can be found with the Administrative Tools.

![](img/d7d2ffa0a76feaab821930e95daace93_729_0.png)

FIGURE 25-1

## WINDOWS SERVICES ARCHITECTURE

Three program types are necessary to operate a Windows Service:
- A service program
- A service control program
- A service configuration program

The service program itself provides the actual functionality you are looking for. With a service control program, it is possible to send control requests to a service, such as start, stop, pause, and continue. With a service configuration program, a service can be installed; it is copied to the file system, written into the registry, and configured as a service. Although .NET components can be installed simply with an xcopy — because they don't need to write information to the registry — installation for services requires registry configuration. A service configuration program can also be used to change the configuration of that service at a later point.

These three ingredients of a Windows Service are discussed in the following subsections.

### Service Program

Before looking at the .NET implementation of a service, let's explore, from an independent point of view, what the Windows architecture of services looks like and what the inner functionality of a service is.

### Service Control Program

As the name suggests, with a service control program, you can control the service. For stopping, suspending, and resuming the service, you can send control codes to the service, and the handler should react to these events. It is also possible to ask the service about the actual status and to implement a custom handler that responds to custom control codes.

### Service Configuration Program

Because services must be configured in the registry, you can't use xcopy installation with services. The registry contains the startup type of the service, which can be set to automatic, manual, or disabled. You also need to configure the user of the service program and dependencies of the service — for example, the services that must be started before this one can start. All these configurations are made within a service configuration program. The installation program can use the service configuration program to configure the service, but this program can also be used at a later time to change service configuration parameters.

## Classes for Windows Services

In the .NET Framework, you can find service classes in the System.ServiceProcess namespace that implement the three parts of a service:
- You must inherit from the ServiceBase class to implement a service. The ServiceBase class is used to register the service and to answer start and stop requests.
- The ServiceController class is used to implement a service control program. With this class, you can send requests to services.
- The ServiceProcessInstaller and ServiceInstaller classes are, as their names suggest, classes to install and configure service programs.

Now you are ready to create a new service.

## CREATING A WINDOWS SERVICE PROGRAM

The service that you create in this chapter hosts a quote server. With every request that is made from a client, the quote server returns a random quote from a quote file. The first part of the solution uses three assemblies, one for the client and two for the server. Figure 25-4 gives an overview of the solution. The assembly QuoteServer holds the actual functionality. The service reads the quote file in a memory cache, and answers requests for quotes with the help of a socket server. The QuoteClient is a WPF rich-client application. This application creates a client socket to communicate with the QuoteServer. The third assembly is the actual service. The QuoteService starts and stops the QuoteServer; the service controls the server.

![](img/d7d2ffa0a76feaab821930e95daace93_731_0.png)

FIGURE 25-4

### Creating Core Functionality for the Service

You can build any functionality in a Windows Service, such as scanning for files to do a backup or a virus check or starting a WCF server. However, all service programs share some similarities. The program must be able to start (and to return to the caller), stop, and suspend. This section looks at such an implementation using a socket server.

With Windows 7, the Simple TCP/IP Services can be installed as part of the Windows components. Part of the Simple TCP/IP Services is a "quote of the day," or qotd, TCP/IP server. This simple service listens to port 17 and answers every request with a random message from the file <windir>\system32\drivers\etc\quotes. With the sample service, a similar server will be built. The sample server returns a Unicode string, in contrast to the good-old qotd server that returns an ASCII string.

First, create a Class Library called QuoteServer and implement the code for the server. The following walks through the source code of your QuoteServer class in the file QuoteServer.cs:

```
```csharp
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.IO;
using System.Linq;
using System.Net;
using System.Net.Sockets;
using System.Text;
using System.Threading;

namespace Prox.ProSharp.WinServices
{
    public class QuoteServer
    {
        private TcpListener listener;
        private int port;
        private string filename;
        private List<string> quotes;
        private Random random;
        private Thread listenerThread;
```
```

The constructor QuoteServer() is overloaded so that a filename and a port can be passed to the call. The constructor where just the file name is passed uses the default port 7890 for the server. The default constructor defines the default filename for the quotes as quotes.txt:

```
```csharp
public QuoteServer()
    : this("quotes.txt")
{
}
public QuoteServer(string filename)
    : this(filename, 7890)
{
}
public QuoteServer(string filename, int port)
{
    this.filename = filename;
    this.port = port;
}
```
```
