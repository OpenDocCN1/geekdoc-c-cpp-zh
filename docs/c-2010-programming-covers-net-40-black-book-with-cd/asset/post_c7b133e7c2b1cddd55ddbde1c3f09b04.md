
![](img/e073a4882197be4ab61103cbe0bcb394_1001_0.png)

**Figure 19.3: Displaying the WCF Architecture**

In Figure 19.3, you can see the following layers of the WCF architecture:

- Contracts
- Service Runtime
- Messaging
- Hosting and Activation

Let’s discuss these layers in detail.

### The Contracts Layer

The contracts layer provides information about the different features of a message system. A system that involves sending and receiving messages from one endpoint to another is known as message system. The contracts layer contains the following four components:

- Data contract — Describes message parameters. These parameters are XML-based and are used to create a message that is formed or consumed by WCF services.
- Message contract — Defines a specific part of a message, using SOAP.
- Service contract — Provides specific information to a client, which enables the client to understand what the service offers.
- Policy and binding — Specifies the transport media, such as HTTP or Transmission Control Protocol (TCP). It also includes some of the security requirements necessary for communication.

### The Service Runtime Layer

The service runtime layer specifies and manages different behaviors of a WCF service that occur during its operation, such as consuming or hosting the services. The following is a list of behaviors managed by the service runtime layer:

- Throttling behavior — Controls the number of messages processed by a WCF service
- **Error behavior** — Specifies the action to be taken if a message displays an error during service runtime
- **Metadata behavior** — Checks the processing of metadata to ensure that it is available to the external clients
- **Instance behavior** — Specifies the number of service instances of a WCF service made available to the client
- **Message Inspection** — Inspects all or a part of a message during service runtime, to confirm whether the messages are valid or not
- **Transaction behavior** — Changes the state of a transaction, if a failure occurs
- **Dispatch behavior** — Determines how a message is handled and processed by the WCF infrastructure
- **Concurrency behavior** — Controls parallel functions that are running at the time of client and server communication
- **Parameter Filtering** — Filters the parameters of a method before it is invoked

### The Messaging Layer

The messaging layer provides information about different channels, which are required at the time of processing a message. These channels help in message processing, and the messaging layer deals with messages that need to be communicated. The messaging layer uses two channels to communicate the messages, transport and protocol. The transport channel is used to read, write, and convert messages into an XML format; while the protocol channel includes the protocols used to process a message. Some of the protocols are WS-Security and WS-Reliability.

### The Hosting and Activation Layer

The hosting and activation layer renders various options for the services in which they can be activated as well as hosted. In this layer, a service can be hosted using the Internet Information Service (IIS) or Windows Activation Service (WAS). WCF provides the following three options for hosting services:

- **Self-hosting the service in its own application domain** — Hosts the services in its own application domain. Some applications often need to expose services from their own process rather than relying on the one provided by Windows. When a client requests for a WCF service, the process that hosts it must be in the running state. A WCF service hosted in this manner runs in a Windows service and allows it to start when a system boots or when a WCF service is hosted in a Graphical User Interface (GUI) application. The implementation of the hosting and activation layer is described with the help of an example later in this chapter.
- **Host in the application domain and process provided by the IIS Server** — Relies on a virtual directory to host a WCF service. When you use WCF to host services offered by IIS, they are automatically integrated into ASP.NET. This integration allows WCF to take advantage of the inherited features of ASP.NET. One of the biggest advantages of using IIS is that you do not need any hosting code as part of the WCF service to host it. The WCF service is automatically activated by IIS using traditional Web hosting techniques.
- **Host in the application domain and process provided by the WAS Server** — Specifies a new process activation mechanism that retains the process model of IIS and hosting features. WAS automatically activates WCF applications when they are deployed on a computer that is running WAS.

You can select a different hosting environment depending on the various scenarios and key benefits, which are described in Table 19.1:

**Table 19.1: Showing the Various Scenarios to Select the Right Hosting Environment**

| Hosting Environment | Common Scenarios | Key Benefits and Limitations |
|---|---|---|
| Self-hosted | • Using console applications during developments<br>• Accessing a WCF service using Rich Winform and WPF client applications | • Allows you to easily deploy WCF services<br>• Does not provide an enterprise solution for WCF services |
| IIS | • Running a WCF service with ASP.NET content<br>• Running a WCF service on the Internet using various transport protocols<br>• Running a WCF service and the ASP.NET content simultaneously by using the HTTP protocol | • Supports integration of ASP.NET with IIS content<br>• Provides WAS benefits<br>• Allows message-based activation<br>• Manages process recycling idle-time<br>• Monitors process health<br>• Uses HTTP protocol only |
| WAS | • Running a WCF service without installing IIS on the Internet using various transport protocols | • Does not require IIS<br>• Manages idle-time<br>• Monitors process health<br>• Allows message-based activation<br>• Works with protocols, such as HTTP, TCP, MSMQ, and named pipes |
| Windows service or NT service | • Hosting WCF service outside IIS | • Provides secure environment<br>• Controls the service process lifetime using an Operating System (OS) |

Next, you learn about WCF endpoints.

### WCF Endpoints

A WCF service is connected to its clients through an endpoint, which contains a contract, an address, and a binding. A contract, in general, is an agreement between two or more parties. Similarly, in WCF services, a contract defines a protocol to determine how a client should communicate with the service. Technically, it describes the parameters and the return values for a method. A contract also describes the operations that can be invoked using an endpoint. It is identified using the name of the interface that defines the operations.

The location from where an endpoint can be accessed is specified by an address, known as the Uniform Resource Locator (URL). The binding defines how the endpoint's operations can be invoked. It specifies how the data is transferred between the service and its client, i.e. what communication protocols are used to access the services and what types of security model should be used in the WCF services.

A WCF service includes predefined bindings for most common communication protocols, such as SOAP over HTTP, SOAP over TCP, and SOAP over Message Queues. When a client wants to access a WCF service through an endpoint, it accesses the specified binding. Figure 19.4 displays the three main components of an endpoint:

![](img/e073a4882197be4ab61103cbe0bcb394_1003_0.png)

**Figure 19.4: Displaying the Endpoint Architecture**

When a message is processed and encoded at the transport channel, it is sent to each protocol channel for further processing, until it reaches at the top of the channel stack. Finally, the message is dispatched to the WCF service implementation by the dispatcher.

In WCF, bindings are represented by the System.ServiceModel.Channels.Binding class. All bindings must be derived from this base class. Table 19.2 shows a list of system-provided bindings:

**Table 19.2: Showing the WCF System-Provided Bindings**

| Binding Class | Binding Element | Description |
|---|---|---|
| BasicHttpBinding | <basicHttpBinding> | Supports basic interoperability and is used for first-generation Web services. It provides security to Web services using transport protocols, such as HTTP and HTTPS. |
| WSHttpBinding | <wsHttpBinding> | Supports the WS-* functionality and distributed transactions with reliable and secure sessions using the SOAP security. It uses HTTP and HTTPS transport protocols for communication. |
| WSDualHttpBinding | <wsDualHttpBinding> | Supports duplex messaging, unlike the WSHttpBinding binding. |
| WSFederationHttpBinding | <wsFederationHttpBinding> | Supports secure and interoperable sharing identities across multiple computers for authentication and authorization. |
| NetTcpBinding | <netTcpBinding> | Supports all predefined bindings prefixed with the name Net. These bindings use a binary encoding to communicate with .NET applications, which is faster than any text encoding. |
| NetPeerTcpBinding | <netPeerTcpBinding> | Supports a binding for peer-to-peer communication. |
| NetNamedPipesBinding | <netNamedPipesBinding> | Supports an optimized communication between different processes on the same system. |
| NetMsmqBinding | <netMsmqBinding> | Supports queued communication, where messages are sent to a message queue. |
| MsmqIntegrationBinding | <msmqIntegrationBinding> | Enables applications to send and receive messages to and from the existing MSMQ applications. |
| CustomBinding | <customBinding> | Customizes the transport protocol and security requirements. |

### Service Contracts

A service contract defines the operations that a WCF service can support, the message exchange pattern the service contract uses, and the format of each message. It generates a service description so that every WCF service can implement at least one service contract. To create a service contract, you first need to define an interface, which contains the methods that represent the service operations. Next, you need to apply the ServiceContractAttribute attribute to the interface to indicate that it is a service contract. The methods that represent the operations of a service contract use the OperationContractAttribute attribute, as shown in the following code snippet:

```
[ServiceContract]
public interface IRailwayReservation
{
    [OperationContract]
    bool ReserveSeat(SeatReservation seatReservation);
}
```
