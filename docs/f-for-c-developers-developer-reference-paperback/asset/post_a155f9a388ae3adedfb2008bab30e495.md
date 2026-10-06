
Before the code is presented, you need to retrieve the default key by clicking the Access Key button at the bottom of the page, as shown in Figure 8-39.

![](img/63aaf94e22830ab98ce16c5946be8ef6_538_0.png)

**FIGURE 8-39** Service bus configuration UI

Figure 8-40 shows the default key.

![](img/63aaf94e22830ab98ce16c5946be8ef6_538_1.png)

**FIGURE 8-40** Default key for the service

CHAPTER 8 Cloud and Service Programming with F# 519

These setup steps provide the service namespace, service bus queue, and user secret. Creating a cloud queue structure is similar to the procedure for creating a service bus. It can be done using the Cloud Services menu item, which you can see in Figure 8-36.

# Service-Side Code

The next sample code creates an echo service. The service listens for incoming messages, receives a message, and sends back that same message. The service code has its configuration file, App.config, and a .fs file defines how to communicate with the Azure cloud and the service's version file, which is 1.7.0.0 in Listing 8-23.

**LISTING 8-23** Configuration file for a service bus

```xml
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceBus.Samples.EchoService">
        <endpoint contract="Microsoft.ServiceBus.Samples.EchoContract"
          binding="netTcpRelayBinding" />
      </service>
    </services>
    <extensions>
      <add name="netTcpRelayBinding"
          type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement,Microsoft.ServiceBus,Version=1.7.0.0,Culture=neutral,PublicKey=31bf386ad364e35" />
    </extensions>
  </system.serviceModel>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0" />
  </startup>
</configuration>
```

The service code, shown in Listing 8-24, defines a contract interface named **EchoContract** and a channel interface named **EchoChannel**. The service namespace, service queue name, and *userSecret* are created during the setup step. You can use F5 to run the program.

**LISTING 8-24** Echo service code using an Azure service bus

```fsharp
// Learn more about F# at http://fsharp.org
namespace Microsoft.ServiceBus.Samples

open Microsoft.ServiceBus
open System.ServiceModel
```

```fsharp
[ServiceContract(
    Name = "IEchoContract",
    Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
type IEchoContract = interface
    [OperationContract]>
    abstract member Echo : msg:string -> string
end

type IEchoChannel = interface
    inherit IEchoContract
    inherit IClientChannel
end

[ServiceBehavior(
    Name = "EchoService",
    Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
type EchoService() = class
    interface IEchoContract with
        member this.Echo(msg) =
            printf("%s" msg)
            msg
end

module Program =
    [EntryPoint]
    let Main(args) =
        let serviceNamespace = "testServiceBus0"
        let userService = "owner"
        let userSecret = "<your account key>"

        // create the service credential
        let sharedServiceCredential = TransportClientEndpointBehavior()
        sharedServiceCredential.TokenProvider <-
            Token.CreateSecretTokenProvider(userService, userSecret)

        // set up the service host
        let address = ServiceEnvironment.CreateUri("sb://{serviceNamespace}/EchoService")
        let host = new ServiceHost<EchoService>(address)
        let serviceRegistrySettings = new RegistrySettings(Discovery.Public)

        // setup endpoints
        for endpoint in host.Description do
            endpoint.Behaviors.Add(serviceRegistrySettings)
            endpoint.Behaviors.Add(sharedServiceCredential)

        // open the service host
        host.Open()

        Console.WriteLine("Service address: " + address.ToString())
        Console.WriteLine("Press [Enter] to exit")
        Console.ReadLine()

        // close the host
        host.Close()
```

Note The interface, class, and struct keywords in the type definition are optional. The following two interface snippets are:

```fsharp
type IA = interface
    abstract member : int -> int

type IB = interface
    abstract : int -> int
```

# Client-Side Code

Like server-side code, the client-side code's configuration is located in App.config and has some .fs code. The service bus DLL is version 1.7.0.0. The client-side code—it sends a message to the service. In Listing 8-26, a service interface named EchoContract and a channel interface named EchoChannel are defined. The message is sent via the created channel.

**LISTING 8-25** Client-side configuration file

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.serviceModel>
    <client>
      <endpoint name="RelayEndpoint" contract="Microsoft.ServiceBus.Samples.EchoContract" binding="netTcpRelayBinding" />
    </client>
    <extensions>
      <add name="netTcpRelayBinding" type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement,Microsoft.ServiceBus,Version=1.7.0.0,Culture=neutral,PublicKey=31bf386ad364e35" />
    </extensions>
  </system.serviceModel>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0" />
  </startup>
</configuration>
```

**LISTING 8-26** Client-side code for the service bus

```fsharp
// Learn more about F# at http://fsharp.org
namespace Microsoft.ServiceBus.Samples

open System
open Microsoft.ServiceBus
open System.ServiceModel

[ServiceContract(
  Name = "IEchoContract",
  Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
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
    ServiceBusEnvironment.Connectivity.Mode <- ConnectivityMode.AutoDetect

    let serviceNamespace = "testServiceBus0"
    let issuerName = "owner"
    let issuerSecret = "<your account key>"

    let serviceUri = ServiceBusEnvironment.CreateUri("sb://" + serviceNamespace)

    let sharedSecretBusCredential = new TransportClientEndpointBehavior()
    sharedSecretBusCredential.TokenProvider <-
      Token.CreateSharedSecretTokenProvider(issuerName, issuerSecret)

    let channelFactory = new ChannelFactory<IEchoChannel>((
      "RelayEndpoint",
      new EndpointAddress(serviceUri)))

    channelFactory.Endpoint.Behaviors.Add(sharedSecretBusCredential)
    let channel = channelFactory.CreateChannel()
    channel.Open()

    Console.WriteLine("Enter text to echo (or [Enter] to exit):")
    let mutable input = Console.ReadLine()
    while (input <> String.Empty) do
        try
            Console.WriteLine("Server echoed: {0}", channel.Echo(input))
        with
        as e->
            Console.WriteLine("Error: " + e.Message)
        input <- Console.ReadLine()

    channel.Close()
    channelFactory.Close()
```

This simple communication mechanism is used to implement the cloud GA sample, which exchanges the best individuals among populations. The cloud GA sample is shown in next section.

# Genetic Algorithms in the Cloud

When talking about how to parallelize the GA in the cloud, there are two choices. One is to make the parallel work on the chromosome level, and the other is to make it work on the population level. Because the communication cost in the cloud environment cannot be ignored, implementation takes the population-level option, which means each virtual host on the cloud runs a population. The best chromosome in one population is selected and injected into another population or populations. After several iterations, all of the populations are supposed to converge at the same area and, we hope, that is the optimal solution is located.
