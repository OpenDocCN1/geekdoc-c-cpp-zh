
The default values are listed in the following table.

| LEASE CONFIGURATION | DEFAULT VALUE (SECONDS) |
|---|---|
| LeaseTime | 300 |
| RenewOnCallTime | 120 |
| SponsorshipTimeout | 120 |
| LeaseManagerPollTime | 10 |

## Classes Used for Lifetime Management

The ClientSponsor class implements the ISponsor interface. It can be used on the client side for lease extension. With the ILease interface, you can get all information about the lease, all the lease properties, and the current lease time and state. The state is specified with the LeaseState enumeration. With the LifetimeServices utility class, you can get and set the properties for the lease of all remote objects in the application domain.

### Getting Lease Information Example

In this small code example, the lease information is accessed by calling the GetLifetimeService() method of the transparent proxy. For the ILease interface, you have to declare the namespace System.Runtime.Remoting.Lifetime. For the class UrlAttribute, you have to import the namespace System.Runtime.Remoting.Activation.

The leasing mechanism can only be used with stateful (client-activated and singleton) objects. Single-call objects are instantiated with every method call anyway, so the leasing mechanism doesn't apply. To offer client-activated objects with the server, you can change the remoting configuration to a call to RegisterActivatedServiceType():

```csharp
RemotingConfiguration.ApplicationName = "Hello";
RemotingConfiguration.RegisterActivatedServiceType(typeof(Hello));
```

In the client application, the instantiation of the remote object must be changed, too. Instead of using the method Activator.GetObject(), Activator.CreateInstance() is used to invoke client-activated objects:

```csharp
ChannelServices.RegisterChannel(new TcpClientChannel(), true);
object[] attrs = { new UrlAttribute("tcp://localhost:8086/Hello") };
Hello obj = (Hello)Activator.CreateInstance(typeof(Hello), null, attrs);
```

To show the leasing time, you can use the ILease interface returned by calling GetLifetimeService() from the proxy object:

```csharp
ILease lease = (ILease)obj.GetLifetimeService();
if (lease != null)
{
    Console.WriteLine("Lease Configuration:");
    Console.WriteLine("InitialLeaseTime: {0}", lease.InitialLeaseTime);
    Console.WriteLine("RenewOnCallTime: {0}", lease.RenewOnCallTime);
    Console.WriteLine("SponsorshipTimeout: {0}", lease.SponsorshipTimeout);
    Console.WriteLine(lease.CurrentLeaseTime);
}
```

### Changing Default Lease Configurations

The server itself can change the default lease configuration for all remote objects of the server using the System.Runtime.Remoting.Lifetime.LifetimeServices utility class:

```csharp
LifetimeServices.LeaseTime = TimeSpan.FromMinutes(10);
LifetimeServices.RenewOnCallTime = TimeSpan.FromMinutes(2);
```

## HOSTING SERVERS IN ASP.NET

Up to this point, all the sample servers have been running in self-hosted .NET servers. A self-hosted server must be launched manually. A .NET Remoting server can also be started in a lot of other application types. In a Windows Service, the server can be automatically started at boot time, and in addition the process can run with the credentials of the system account. For more details on Windows Services, see Chapter 25, “Windows Services.”

There’s special support for .NET Remoting servers for ASP.NET. ASP.NET can be used for the automatic startup of remote servers. ASP.NET-hosted Remoting uses a different file for configuration than EXE-hosted applications, but it has the same syntax.

To use the infrastructure from the Internet Information Services (IIS) and ASP.NET, you have to create a class that derives from System.MarshalByRefObject and has a default constructor. The code used earlier for the server to create and register the channel is no longer necessary; that’s done by the ASP.NET runtime. You have to create only a virtual directory on the Web server that maps a directory into which you put the configuration file Web.config. The assembly of the remote class must reside in the bin subdirectory.

To configure a virtual directory on the web server, you can use the IIS MMC. Selecting the Default Web Site and opening the Action menu creates a new Virtual Directory.

The configuration file Web.config on the web server must be put in the home directory of the virtual web site. With the default IIS configuration, the channel that will be used listens to port 80:

```xml
<configuration>
    <system.runtime.remoting>
        <application>
            <service>
                <wellknown mode="SingleCall"
                    type="Wrox.ProcSharp.Remoting.Hello, RemoteHello"
                    objectUri="HelloService.soap" />
            </service>
        </application>
    </system.runtime.remoting>
</configuration>
```

> If the remoting object is hosted within IIS, the name of the remote object must end either with `.soap` or `.rem`, depending on the type of formatter that is used (SOAP or the binary).

The client can now connect to the remote object using the following configuration file. The URL that must be specified for the remote object here is the web server localhost, followed by the web application name RemoteHello (specified when creating the virtual web site), and the URI of the remote object HelloService.soap that is defined in the file Web.config. It’s not necessary to specify the port number 80, because that’s the default port for the HTTP protocol. Not specifying a `<channels>` section means that the delay-loaded HTTP channel from the configuration file machine.config is used:

```xml
<configuration>
    <system.runtime.remoting>
        <application>
            <client url="http://localhost/RemoteHello">
                <wellknown type="Wrox.ProcSharp.Remoting.Hello, RemoteHello"
                    url="http://localhost/RemoteHello/HelloService.soap" />
            </client>
        </application>
    </system.runtime.remoting>
</configuration>
```

![](img/d7d2ffa0a76feaab821930e95daace93_1759_0.png)

## CLASSES, INTERFACES, AND SOAPSUDS

In the .NET Remoting examples you have seen so far, you have always copied the assembly of the remote object not only to the server but also to the client application. This way the MSIL code of the remote object is on both the client and the server system, although in the client application only the metadata is needed. However, copying the remoting object assembly means that it’s not possible for the client and the server to be programmed independently. A much better way to use just the metadata is to use interfaces or the Soapsuds.exe utility instead.

### Interfaces

You get a cleaner separation of the client and server code by using interfaces. An interface simply defines the methods without implementation. This way the contract (the interface) is separated from the implementation, and just the contract is needed on the client system. Here are the necessary steps for using an interface:

- 1. Define an interface that will be placed in a separate assembly.
- 2. Implement the interface in the remote object class. To do this, the assembly of the interface must be referenced.
- 3. On the server side no more changes are required. The server can be programmed and configured in the usual way.
- 4. On the client side, reference the assembly of the interface instead of the assembly of the remote class.
- 5. The client can now use the interface of the remote object rather than the remote object class. The object can be created using the Activator class as it was done earlier. You can’t use the new operator in this way, because the interface itself cannot be instantiated.

The interface defines the contract between the client and server. The two applications can now be developed independently of each other. If you also stick to the old COM rules about interfaces (that interfaces should never be changed), you will not have any versioning problems.

### Soapsuds

You can also use the Soapsuds utility to get the metadata from an assembly if an HTTP channel and the SOAP formatter are used. Soapsuds can convert assemblies to XML schemas and XML schemas to wrapper classes—it also works in the other direction.

The following command converts the type Hello from the assembly RemoteHello to the assembly HelloWrapper, where a transparent proxy is generated that calls the remote object:

```text
soapsuds -types:Wrox.ProCSharp.Remoting.Hello,RemoteHello -oa:HelloWrapper.dll
```

With Soapsuds you can also get the type information directly from a running server, if the HTTP channel and the SOAP formatter are used:

```text
soapsuds -url:http://localhost:6792/hello/hipwsdl -oa:HelloWrapper.dll
```

In the client, you can now reference the generated assembly instead of the original one. Some of the Soapsuds options are listed in the following table.
