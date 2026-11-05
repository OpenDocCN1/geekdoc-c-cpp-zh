# Explanation

2. The main three components of a Remoting Framework are :

+   1. C# Remotable Object
+   2. C# Remote Listener Application - (listening requests for Remote Object)
+   3. C# Remote Client Application - (makes requests for Remote Object)

3. The Remote Object is implemented in a class that derives from System.MarshalByRefObject.

![](bbox=[0.12, 0.38, 0.92, 0.6])

Fig. 24.2.1 NET remoting frame work

Above Fig. 24.2.1 depicts workflow of .NET Remoting.

+   - When a client calls the Remote method, actually the client does not call the methods directly. It receives a proxy to the remote object and is used to invoke the method on the Remote Object.

Once the proxy receives the method call from the Client, it encodes the message using appropriate formatter (Binary Formatter or SOAP Formatter) according to the Configuration file. After that it sends the call to the Server by using selected Channel (TepChannel or HttpChannel).

The Server side channel receives the request from the proxy and forwards it to the Server on Remoting system, which locates and invokes the methods on the Remote Object. When the execution of remote method is complete, any results from the call are returned back to the client in the same way.

Before an object instance of a Remotable type can be accessed, it must be created and initialized by a process known as Activation. Activation is categorized in two models , they are Client-activated Objects and Server-activated Objects.