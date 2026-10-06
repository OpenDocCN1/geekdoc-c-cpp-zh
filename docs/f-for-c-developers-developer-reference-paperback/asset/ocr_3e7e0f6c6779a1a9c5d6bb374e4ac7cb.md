```
</system.serviceModel>
<startup>
  <supportedRuntime version="v4.0" sku=".Framework,Version=v4.0" />
</startup>
</configuration>
```

# **LISTING 8-26** Client-side code for the service bus service

```
// Learn more about F# at http://fsharp.net

namespace Microsoft.ServiceBus.Samples

open System
open Microsoft.ServiceBus;
open System.ServiceModel;

[ServiceContract(
  Name = "IEchoContract",
  Namespace = "#samples.microsoft.com/ServiceModel/Relay/")
type IEchoContract = interface
  [OperationContract]
    abstract member Echo : msg -> string
end

type IEchoChannel = interface
  inherit IEchoContract
  inherit IClientChannel
end

module Program =
  [EntryPoint]
  let Main(args) =
    ServiceBusEnvironment.SystemConnectivity.Mode <- ConnectivityMode.AutoDetect;

    let serviceNamespace = "testServiceBus0"
    let issuerName = "owner"
    let issuerSecret = "<your account key>"

    let serviceUri = ServiceBusEnvironment.CreateServiceUri("sb",
      serviceNamespace,)

    let sharedSecretBusCredential = new TransportClientEndpointBehavior();
    sharedSecretBusCredential.TokenProvider <-
      Token.CreateSharedSecretTokenProvider(issuerName, issuerSecret);

    let channelFactory = new ChannelFactory<IEchoChannel>((
      "RelayEndpoint",
      new EndpointAddress(serviceUri)));
```