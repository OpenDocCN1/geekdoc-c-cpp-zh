
| Table 35.2: Noteworthy Public Methods of the AppDomain Class |
| Method | Description |
| CreateInstanceFromAndUnwrap() | Builds a new instance, which is not wrapped, of a specified type, where the source is specified in the specified assembly file |
| ExecuteAssembly() | Executes the assembly contained in the specified file |
| GetAssemblies() | Obtains the assemblies that have been loaded into the application domain |
| GetCurrentThreadId() | Obtains the current thread identifier |
| InitializeLifetimeService() | Starts providing lifetime service to an AppDomain object at the time of its initialization |
| IsFinalizingForUnload() | Indicates whether or not the application domain is unloading, and the objects it contains are being finalized by the CLR |
| Load() | Loads an assembly into the application domain |
| SetAppDomainPolicy() | Establishes a security policy for an application domain |
| SetCachePath() | Sets a directory path to store the copies of assemblies |
| SetShadowCopyFiles() | Turns on shadow-copying |
| Unload() | Unloads the specified application domain |

Table 35.3 lists the noteworthy public events of the AppDomain class:

| Table 35.3: Noteworthy Public Events of the AppDomain Class |
| Event | Description |
| AssemblyLoad | Occurs when an assembly is loaded |
| AssemblyResolve | Occurs when the resolution of an assembly fails |
| DomainUnload | Occurs when an AppDomain is about to be unloaded |
| ProcessExit | Occurs on the default application domain when the default application domain's parent process exits |
| ResourceResolve | Occurs when the resolution of a resource fails |
| TypeResolve | Occurs when the resolution of a type fails |

## Remotable and Non-Remotable Objects

The .NET remoting architecture divides objects into two categories – non-remotable and remotable. An object belongs to the remotable category if and only if instances of the object can cross .NET remoting boundaries or can be accessed by other objects across .NET remoting boundaries. If an object does not satisfy either of these conditions, then the object falls under the category of non-remotable objects. In other words, non-remotable objects are those objects that cannot be accessed outside their own application domains. The non-remotable objects are designed for use within the same AppDomain in which they were created and are always accessed directly from that AppDomain. Furthermore, the non-remotable objects cannot be copied or represented in another AppDomain.

Unlike non-remotable objects, remotable objects are accessible outside their own AppDomain using a proxy. The .NET remoting architecture broadly divides the remotable objects into two categories – marshal-by-value (MBV) and marshal-by-reference (MBR). Let’s discuss these two categories in the following sections.

## Marshal-By-Value

Marshalling is a process of packaging and sending method calls between objects and across application boundaries using the serialization and deserialization mechanisms. The MBV objects declare their serializability by either implementing the ISerializable interface or by being marked with the SerializableAttribute attribute, which in turn, serializes the object automatically. The ISerializable interface belongs to the System.Runtime.Serialization namespace. It provides the GetObjectData() method to populate the SerializationInfo object with the data that has to be serialized in a remote object. The MBV objects are copied and passed from the server's AppDomain to the client's AppDomain.

## Marshal-By-Reference

MBR objects are accessed on the client side using a proxy. The client only needs to hold the reference of the objects. When a client creates an instance of the MBR object in its own application domain, the .NET remoting framework creates a proxy to represent the MBR object and sends a reference of that proxy to the client. The client then makes calls on the proxy. The .NET remoting marshals those calls to the application domain of the remote object and invokes the call. To define an MBR object, you need to use the System.MarshalByRefObject class.

> NOTE
> If a client and an MBR object are in the same application domain, the .NET remoting framework returns a direct reference of the MBR object to the client without marshalling.

The MarshalByRefObject class enables access to objects across application domain boundaries in applications that support remoting. The class hierarchy of the MarshalByRefObject class is shown as follows:
System.Object
System.MarshalByRefObject

Table 35.4 lists the noteworthy public methods of the MarshalByRefObject class:

| Table 35.4: Noteworthy Public Methods of the MarshalByRefObject Class |
| Method | Description |
| CreateObjRef() | Creates an object that contains all the relevant information required to generate a proxy used to communicate with a remote object |
| GetLifetimeService() | Retrieves the lifetime service of the current object |
| InitializeLifetimeService() | Starts providing a lifetime service to an object |

Before instantiating a remotable object, you need to create and initialize it by a process called activation. MBR supports two types of activation, server activation and client activation.

> NOTE
> MBV objects do not require any activation process because they are copied using the serialization process and activated using deserialization.

The two types of MBR activation are described as follows:

- Server Activation – Activates the remote objects that exist on a server. These remote objects are also called Server Activated Objects (SAO). You cannot create an SAO object by using the new keyword. An SAO object is activated when a client calls a method on the proxy object. The SAO objects are activated using the following two modes:
  - Singleton – Uses a single object to serve the requests of all clients. An instance of Singleton object is created when the first client tries to access it. After that the subsequent client calls are channeled to the same Singleton object. The Singleton object maintains the session state across requests or method calls.
  - SingleCall – Creates an object to serve a single client request. When you configure an object as SingleCall, the .NET Framework activates a new instance of this object for every method invocation made by a client, after which it is garbage collected for recycling. The SingleCall mode handles only one request at a time and does not maintain a session state between requests; therefore, it is called stateless.

- Client Activation – Activates the remote objects that exist on a client. These remote objects are also called Client Activated Objects (CAO). To handle CAO objects, the .NET Framework assigns a uniform resource identifier (URI) to each instance of a CAO object. The CAO objects are created on the server corresponding to the client requests. They maintain a state for each client they are serving but they cannot share a common state.

> NOTE
> SAO objects that are published at a Uniform Resource Locator (URL) outside the application domain are called well-known objects.

Let’s now discuss how to set remote communication.

## Setting Up Remoting Communication

In .NET Framework, to set communication between remote objects, you need to use the RemotingConfiguration class. The methods contained in the RemotingConfiguration class help in configuring the remoting architecture and registering different objects to a remote system. The class hierarchy of the RemotingConfiguration class is shown as follows:

```
System.Object
System.Runtime.Remoting.RemotingConfiguration
```

You can find the noteworthy public properties of the RemotingConfiguration class in Table 35.5:

Table 35.5: Noteworthy Public Properties of the RemotingConfiguration Class
| Property | Description |
| ApplicationId | Obtains the ID of the currently executing application |
| ApplicationName | Obtains the name of a remote application |
| ProcessId | Obtains the ID of the currently executing process |

Table 35.6 describes the noteworthy public methods of the RemotingConfiguration class:

Table 35.6: Noteworthy Public Methods of the RemotingConfiguration Class
| Method | Description |
| Configure() | Reads the configuration file and configures the remoting infrastructure |
| GetRegisteredActivatedClientTypes() | Retrieves an array of object types registered on the client end as types that can be activated remotely |
| GetRegisteredActivatedServiceTypes() | Retrieves an array of object types registered on the service end as types that can be activated on request from a client |
| GetRegisteredWellKnownClientTypes() | Retrieves an array of object types registered on the client end as well-known types |
| GetRegisteredWellKnownServiceTypes() | Retrieves an array of object types registered on the service end as well-known types |
| IsActivationAllowed() | Returns a Boolean value indicating whether the specified type is allowed to be client activated |
| IsRemotelyActivatedClientType() | Checks whether the specified object type is registered as a remotely activated client type |
| IsWellKnownClientType() | Checks whether the specified object type is registered as a well-known client type |
| RegisterActivatedClientType() | Registers an object type on the client end as a type that can be activated on the server |
| RegisterActivatedServiceType() | Registers an object type on the service end as a type that can be activated on request from a client |
| RegisterWellKnownClientType() | Registers an object type on the client end as a well-known type (SingleCall or Singleton) |
