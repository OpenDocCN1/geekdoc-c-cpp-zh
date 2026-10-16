
```xml
<behaviors>
    <serviceBehaviors>
        <behavior name="StateServiceSample.Service1Behavior">
            <serviceMetadata httpGetEnabled="True"/>
            <serviceDebug includeExceptionDetailInFaults="False" />
        </behavior>
    </serviceBehaviors>
</behaviors>
</system.serviceModel>
</configuration>
```

If you start the service host with the defined configuration, an exception of type InvalidOperationException is thrown. The error message with the exception gives this error message: Contract Requires Session, but Binding `BasicHttpBinding` Doesn’t Support It or Isn’t Configured Properly to Support It.

Not all bindings support all services. Because the service contract requires a session with the attribute `[ServiceContract(SessionMode=SessionMode.Required)]`, the host fails because the configured binding does not support sessions.

As soon as you change the configuration to a binding that supports sessions (for example, the `wsHttpBinding`), the server starts successfully:

```xml
<endpoint address="" binding="wsHttpBinding" bindingConfiguration="" contract="Wrox.ProCSharp.WCF.IStateService">
</endpoint>
```

With the implementation of the service, you can apply the properties in the following table to the service methods, with the attribute `OperationBehavior`.

| OperationBehavior Property | Description |
|---|---|
| AutoDisposeParameters | By default, all disposable parameters are automatically disposed. If the parameters should not be disposed, you can set the property `AutoDisposeParameters` to false. Then the sender is responsible for disposing the parameters. |
| Impersonation | With the `Impersonation` property, the caller can be impersonated, and the method runs with the identity of the caller. |
| ReleaseInstanceMode | The `InstanceContextMode` defines the lifetime of the object instance with the service behavior setting. With the operation behavior setting, you can override the setting based on the operation. The `ReleaseInstanceMode` defines an instance release mode with the enumeration `ReleaseInstanceMode`. The value `None` uses the instance context mode setting. With the values `BeforeCall`, `AfterCall`, and `BeforeAndAfterCall`, you can define recycle times with the operation. |
| TransactionScopeRequired | With the property `TransactionScopeRequired`, you can specify whether a transaction is required with the operation. If a transaction is required and the caller already flows a transaction, the same transaction is used. If the caller doesn’t flow a transaction, a new transaction is created. |
| TransactionAutoComplete | The `TransactionAutoComplete` property specifies whether the transaction should complete automatically. If the `TransactionAutoComplete` property is set to true, the transaction is aborted if an exception is thrown. The transaction is committed if it is the root transaction and no exception is thrown. |

## Binding

A binding describes how a service wants to communicate. With binding, you can specify the following features:

- Transport protocol
- Security
- Encoding format
- Transaction flow
- Reliability
- Shape change
- Transport upgrade

## Standard Bindings

A binding is composed of multiple binding elements that describe all binding requirements. You can create a custom binding or use one of the predefined bindings that are shown in the following table.

| Standard Binding | Description |
| --- | --- |
| BasicHttpBinding | BasicHttpBinding is the binding for the broadest interoperability, the first-generation web services. Transport protocols used are HTTP or HTTPS; security is available only from the transport protocol. |
| WSHttpBinding | WSHttpBinding is the binding for the next-generation web services, platforms that implement SOAP extensions for security, reliability, and transactions. The transports used are HTTP or HTTPS; for security the WS-Security specification is implemented; transactions are supported, as has been described, with the WS-Coordination, WS-AtomicTransaction, and WS-BusinessActivity specifications; reliable messaging is supported with an implementation of WS-ReliableMessaging. WS-Profile also supports Message Transmission Optimization Protocol (MTOM) encoding for sending attachments. You can find specifications for the WS-* standards at http://www.oasis-open.org. |
| WS2007HttpBinding | WS2007HttpBinding derives from the base class WSHttpBinding and supports security, reliability, and transaction specifications defined by the Organization for the Advancement of Structured Information Standards (OASIS). This class offers newer SOAP standards. |
| WSHttpContextBinding | WSHttpContextBinding derives from the base class WSHttpBinding and adds support for a context without using cookies. This binding adds a `ContextBindingElement` to exchange context information. The context binding element was needed with Windows Workflow Foundation (WF) 3.0. |
| `WebHttpBinding` | This binding is used for services that are exposed through HTTP requests instead of SOAP requests. This is useful for scripting clients—for example, ASP.NET AJAX. |
| `WSFederationHttpBinding` | `WSFederationHttpBinding` is a secure and interoperable binding that supports sharing identities across multiple systems for authentication and authorization. |
| `WSDualHttpBinding` | The binding `WSDualHttpBinding`, in contrast to `WSHttpBinding`, supports duplex messaging. |
| `NetTcpBinding` | All standard bindings prefixed with the name `Net` use a binary encoding used for communication between .NET applications. This encoding is faster than the text encoding with WSxxx bindings. The binding `NetTcpBinding` uses the TCP/IP protocol. |
| `NetTcpContextBinding` | Similar to `WSHttpContextBinding`, `NetTcpContextBinding` adds a `ContextBindingElement` to exchange context with the SOAP header. |
| `NetHttpBinding` | This is a new binding since .NET 4.5 to support the Web Socket transport protocol. |
| `NetPeerTcpBinding` | `NetPeerTcpBinding` provides a binding for peer-to-peer communication. |
| `NetNamedPipeBinding` | `NetNamedPipeBinding` is optimized for communication between different processes on the same system. |
| `NetMsmqBinding` | The binding `NetMsmqBinding` brings queued communication to WCF. Here, the messages are sent to the message queue. |
| `MsmqIntegrationBinding` | `MsmqIntegrationBinding` is the binding for existing applications that use message queuing. In contrast, the binding `NetMsmqBinding` requires WCF applications on both the client and server. |
| `CustomBinding` | With a `CustomBinding` the transport protocol and security requirements can be completely customized. |

## Features of Standard Bindings

Depending on the binding, different features are supported. The bindings starting with WS are platform-independent, supporting web services specifications. Bindings that start with the name Net use binary formatting for high-performance communication between .NET applications. Other features are support of sessions, reliable sessions, transactions, and duplex communication; the following table lists the bindings supporting these features.

| Feature | Binding |
|---|---|
| Sessions | WSHttpBinding, WSDualHttpBinding, WSFederationHttpBinding, NetTcpBinding, NetNamedPipeBinding |
| Reliable Sessions | WSHttpBinding, WSDualHttpBinding, WSFederationHttpBinding, NetTcpBinding |
| Transactions | WSHttpBinding, WSDualHttpBinding, WSFederationHttpBinding, NetTcpBinding, NetNamedPipeBinding, NetMsmqBinding, MsmqIntegrationBinding |
| Duplex Communication | WSDualHttpBinding, NetTcpBinding, NetNamedPipeBinding, NetPeerTcpBinding |

Along with defining the binding, the service must define an endpoint. The endpoint is dependent on the contract, the address of the service, and the binding. In the following code sample, a ServiceHost object is instantiated, and the address http://localhost:8080/RoomReservation, a `WSHttpBinding` instance, and the contract are added to an endpoint of the service:

```csharp
static ServiceHost s_host;

static void StartService()
{
    var baseAddress = new Uri("http://localhost:8080/RoomReservation");
    s_host = new ServiceHost(typeof(RoomReservationService));

    var binding1 = new WSHttpBinding();
    s_host.AddServiceEndpoint(typeof(IRoomService), binding1, baseAddress);
    s_host.Open();
}
```

In addition to defining the binding programmatically, you can define it with the application configuration file. The configuration for WCF is placed inside the element `<system.serviceModel>`. The `<service>` element defines the services offered. Similarly, as you’ve seen in the code, the service needs an endpoint, and the endpoint contains address, binding, and contract information. The default binding configuration of `wsHttpBinding` is modified with the `bindingConfiguration` XML attribute that references the binding configuration `wsHttpBinding`. This is the binding configuration you can find inside the `<bindings>` section.
