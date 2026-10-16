# Features of Standard Bindings

Depending on the binding, different features are supported. The bindings starting with WS are platform-independent, supporting web services specifications. Bindings that start with the name Net use binary formatting for high-performance communication between .NET applications. Other features are support of sessions, reliable sessions, transactions, and duplex communication; the following table lists the bindings supporting these features.

| Feature | Binding |
|---|---|
| Sessions | WSHttpBinding, WSDualHttpBinding, WsFederationHttpBinding, NetTcpBinding, NetNamedPipeBinding |
| Reliable Sessions | WSHttpBinding, WSDualHttpBinding, WsFederationHttpBinding, NetTcpBinding |
| Transactions | WSHttpBinding, WSDualHttpBinding, WSFederationHttpBinding, NetTcpBinding, NetNamedPipeBinding, NetMsmqBinding, MsmqIntegrationBinding |
| Duplex Communication | WsDualHttpBinding, NetTcpBinding, NetNamedPipeBinding, NetPeerTcpBinding |

Along with defining the binding, the service must define an endpoint. The endpoint is dependent on the contract, the address of the service, and the binding. In the following code sample, a ServiceHost object is instantiated, and the address http://localhost:8080/RoomReservation, a WsHttpBinding instance, and the contract are added to an endpoint of the service:

```
static ServiceHost s_host;

static void StartService()
{
    var baseAddress = new
Uri("http://localhost:8080/RoomReservation");
    s_host = new ServiceHost(typeof(RoomReservationService));

    var binding1 = new WSHttpBinding();
    s_host.AddServiceEndpoint(typeof(IRoomService), binding1,
baseAddress);
    s_host.Open();
}
```

In addition to defining the binding programmatically, you can define it with the application configuration file. The configuration for WCF is placed inside the element <system.serviceModel>. The <service> element defines the services offered. Similarly, as you’ve seen in the code, the service needs an endpoint, and the endpoint contains address, binding, and contract information. The default binding configuration of wsHttpBinding is modified with the bindingConfiguration XML attribute that references the binding configuration wsHttpBinding. This is the binding configuration you can find inside the <bindings> section,