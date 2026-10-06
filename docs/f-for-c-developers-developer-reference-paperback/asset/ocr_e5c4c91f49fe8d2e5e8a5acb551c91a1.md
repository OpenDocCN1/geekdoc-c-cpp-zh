These setup steps provide the service namespace, service bus queue, and user secret. Creating a cloud queue structure is similar to the procedure for creating a service bus. It can be done using the Cloud Services menu item, which you can see in Figure 8-36.

# Service-Side Code

The next sample code creates an echo service. The service listens for incoming messages, receives a message, and sends back that same message. The service code has its configuration file, App.config, and a .fs file defines how to communicate with the Azure cloud and the service's version file, which is 1.7.0.0 in Listing 8-23.

**LISTING 8-23** Configuration file for a service bus

```
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

```
// Learn more about F# at http://fsharp.org
namespace Microsoft.ServiceBus.Samples

open Microsoft.ServiceBus
open System.ServiceModel
```