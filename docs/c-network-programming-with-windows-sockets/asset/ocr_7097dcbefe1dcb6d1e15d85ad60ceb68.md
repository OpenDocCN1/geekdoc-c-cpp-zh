# # The Services File

The service name to port translation is commonly supported by a flat file database called the services file. A partial listing of a common services file looks like the following:

```
```
# This file contains port numbers for well-known services
# as defined by RFC 1060 (Assigned Numbers).
#
# Format:
# <service name>  <port number>/<protocol>  [aliases...]   [#<comment>]

time            37/tcp    timserver
time            37/udp    timserver
finger          79/tcp
```
```

The lines preceded by a pound sign (#) are comments. Notice the reference to RFC 1060. This Internet Request for Comment outlines some standard well-known ports. This ensures that nobody creates a service that utilizes an already established port number. When you create your own custom servers, you need to allocate a port number between 1024 and 5000 exclusive. The ports from 1024 and below are reserved for universally well-known ports. Often, these ports are allocated to new services when someone invents the new service and distributes the specification through an RFC.

Following the header comment is the listed services. The left-most column contains the name of the service. The next column has the port number and transport-level protocol separated by a forward slash (/). The remaining columns contain aliases for the service. In the preceding example, the time service is recognized as "time" or "timserver." The finger service has no aliases. The transport-level protocol field specifies either User Datagram Protocol or Transmission Control Protocol. This is the type of socket (datagram or stream) that must be used to communicate with the designated service. Note that the time service responds to port 37 on both a UDP and TCP connection. The port number/protocol pair provides for a unique correlation to a service within each transport protocol: this is to say that a service might respond to UDP port 100, and a completely different service might respond to TCP port 100. It's also possible for a specific service to respond to one UDP port and an entirely different TCP port.

> **Tip**
> 
> For custom applications that you produce, it's usually sufficient to simply refer to a service number by its port number. This frees you from having to make an entry in the services table for your custom services. For the sake of flexibility, make your server and client applications configurable with respect to the port numbers they use. Allow the server to listen for connections on a configurable port and make sure that the port to which the client connects is also

![](bbox=[0.86, 0.75, 0.96, 0.84])