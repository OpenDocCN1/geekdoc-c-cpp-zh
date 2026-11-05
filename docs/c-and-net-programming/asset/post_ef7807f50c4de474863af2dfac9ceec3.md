
## Explanation

### 3.1 Server Activated Objects

Server Activated Objects are created only when the client makes the first call to the remote method. That is, when the client asks for the creation of the remote object, only the local proxy is created on the client, the actual remote object on the server is instantiated on the first method call. These proxies can be generated as:

```
// On the Server
RemotingConfiguration.RegisterWellKnownServiceType(
    typeof(RemoteServerObject), "Check",
    WellKnownObjectMode.SingleCall);

// On the Client
IRemoteCom obj = (IRemoteCom)Activator.GetObject(typeof(IRemoteCom),
    "tcp://localhost:1002/Check");
```

- Registration types

  There are two registration types, Singleton and SingleCall, which were explained in earlier section. The basic code for registration is,

  ```
  RemotingConfiguration.RegisterWellKnownServiceType(typeof(RemoteServerObject),
      "Check", WellKnownObjectMode.SingleCall);
  ```

  ```
  RemotingConfiguration.RegisterWellKnownServiceType(
      typeof(RemoteServerObject),
      "Check", WellKnownObjectMode.Singleton);
  ```

- For Server Activated Objects, the proxy object (on the client) and the actual object (on the server) are created at different times.

### 3.2 Client Activated Objects

1. Client activate objects are created on the server immediately upon the client's request.
2. An instance of a Client Activated Object is created every time the client instantiates one, either by the use of new or Activator.CreateInstance(...).

   ```
   // On the Server
   RemotingConfiguration.ApplicationName = "CheckCAO";
   RemotingConfiguration.RegisterActivatedServiceType(typeof(RemoteObjectCAO));

   // On the Client
   RemotingConfiguration.RegisterActivatedClientType(typeof(RemoteObjectCAO),
       "tcp://localhost:1002/CheckCAO");
   obj = new RemoteObjectCAO();
   ```

3. In above code snippets, "localhost" can be replaced with an actual remote machine's IP address.
4. **Which activation to use depends upon different scenarios** are discussed below.
   1. Singleton object reference is used when persistent data is held on the server, and is accessible by all clients.
   2. SingleCall model is used to provide a stateless programming model (the traditional Web services request/response model), or any time there is no need to maintain a persistent object state on the server.
   3. Client activation model is used when the object needs to maintain persistent per-client state information.

## Example

```
/*Illustration of .Net Remoting.
*Here Remoting object will send the maximum of the two integer numbers sent.
Creating Remote Server and the Service classes on
Machine 1:
Please note for Remoting support service (Remote object) should be derived from
MarshalByRefObject.*/

using System;
using System.Runtime.Remoting.Channels; //To support and handle Channel and channel sinks
using System.Runtime.Remoting;
using System.Runtime.Remoting.Channels.Http; //For HTTP channel
using System.IO;

namespace ServersideApp
{
public class TechnicalRemotingServer
{
    public TechnicalRemotingServer()
    {
        // constructor code
    }
}
//Service class
public class Service: MarshalByRefObject
{
public void WriteMessage (int n)
{
if (n%2 == 0)
    Console.WriteLine ("Even");
else
    Console.WriteLine ("Odd");
}
}

//Server Class
public class TechnicalServer
{
public static void Main ()
{
HttpChannel channel = new HttpChannel(8001); //Create a new channel
ChannelServices.RegisterChannel (channel); //Register channel

RemotingConfiguration.RegisterWellKnownServiceType(typeof(Service),
    "Service", WellKnownObjectMode.Singleton);
Console.WriteLine ("Server Available at port number 8001");
Console.WriteLine ("Press enter to Stop the server.");
Console.ReadLine ();
}
}
/* Follow the steps,
1. above file is saved as ServerApp.cs.
2. Create an executable by using Visual Studio.Net command prompt by,
csc /r:system.runtime.remoting.dll /r:system.dll ServerApp.cs
A ServerApp.Exe will be generated in the Class folder.
3. Run the ServerApp.Exe.*/
```

## Output

Server Available at port number 8001
Please press enter to stop the server.

- Settings required on the machines are specified below so as to run the remoting applications.
- In order to check whether the HTTP channel is bound to the port, type http://localhost:8001/Service?WSDL, in the browser, one should see an XML file describing the Service class.
- Before running above URL on the browser, the server (ServerApp.Exe should be running) should be ON.
- Creating Proxy and the Client application on Machine 2
- SoapSuds.exe is a utility which can be used for creating a proxy dll.
- Type below command on Visual Studio.Net command prompt.

  ```
  soapsuds -url:http://<Machine Name where service is running>:8001/Service?WSDL -oa:Server.dll
  ```

This will generate a proxy dll by name Server.dll. This will be used to access remote object.

```
//Client Code
using System;
using System.Runtime.Remoting.Channels; //To support and handle Channel and channel sinks
using System.Runtime.Remoting;
using System.Runtime.Remoting.Channels.Http; //For HTTP channel
using System.IO;
using ServerApp;
namespace ClientSideRemotingApp
{
public class TechnicalClientApp
{
public ClientApp()
{
}
public static void Main (string[] args)
{
HttpChannel channel = new HttpChannel (8002); //Create a new channel
ChannelServices.RegisterChannel (channel); //Register the channel
//Create Service class object
Service svc = (Service) Activator.GetObject (typeof (Service),"http://<Machine name here Service running>:8001/Service"); //Localhost can be replaced by
//Pass Message
svc.WriteMessage (10,20);
}
}
/* Follow the steps,
1. Save the above file as ClientApp.cs.
2. Create an executable by using Visual Studio.Net command prompt by,
csc /r:system.runtime.remoting.dll /r:system.dll ClientApp.cs
A ClientApp.Exe will be generated in the Class folder. Run ClientApp.Exe , one can see the result on Running ServerApp.EXE command prompt.
3. In the same way this can be implemented for TCP channel also. */
```

## 24.9 .NET Remoting Metadata

### Concept

.NET Remoting uses metadata to dynamically create proxy objects.

### Explanation

The proxy objects that are created at the client side have the same members as the original class. The client can obtain the metadata information required to access the remote object in the following ways:

- The .NET assembly of the server object.
- The Remoting object can provide a WSDL (Web Services Description Language) file that describes the object and its methods.
- .NET clients can use the SOAPSUDS utility to download the XML schema from the server (generated on the server) to generate source files or an assembly that contains only metadata, no code.

## 24.10 Object Lifetime, Sponsorship and Leases

1. A **Server Activated Object** that has been registered as SingleCall has a very simple and limited lifetime. It lives for a **single call only**. Thereafter, it is marked by the **Garbage Collector** for removal.
2. The other two types, **Singleton** and **Client Activated Objects**, have their lifetimes managed by a service introduced by the .NET Framework, the **Leased Based Manager**. On the server, the application domain's lease manager determines when a server-side object should be marked for deletion.

   Each application domain has its own lease manager object. For objects that have object references that are transported outside the application, a lease is created. The lease has a lease time; when the lease reaches zero, it expires, and the object is disconnected from the **.NET Remoting Framework**.

   When all the references to the object within the **AppDomain** have been freed, the object will be collected when the next garbage collection occurs.

3. A **sponsor** is an object that plays a vital role in the life time of remote objects. When a **lease expires**, one or more of the lease's sponsors are invoked by the Lease Manager, where they are given the opportunity to renew the lease. If none of the sponsors decides to **renew the lease**, the lease manager removes the lease and the object is garbage collected.
4. The **default settings for the lease manager** are,
   1. five minutes for initial time-to-live
   2. poll every ten seconds, and
   3. add an additional two minutes for every remote call by a client.

   All these values are configurable, by overriding **MarshalByRefObject.InitializeLifetimeService()** to define own values in the remotable object.

5. **Renewing Object Leases and Increasing Life Times**
   1. While objects have a **default lease period**, there are ways and reasons to extend the lease period to keep the object alive. When a client wants to maintain state in the same server object it is always good to renew the object life.
