```
Console.WriteLine("Service address: " + address.ToString());
Console.WriteLine("Press [Enter] to exit");
Console.ReadLine() | ignore
```

```
// close the host service
host.Close()
```

0

Note The interface, class, and struct keywords in the type definition are optional. The following two interface definition snippets are the:

```
type IA =
abstract F : int -> int

type IB = interface
abstract F : int -> int
end
```

# Client-Side Code

Like server-side code, the client-side code's configuration is located in the App.config and has some simple .fs code. The configuration code is shown in Listing 8-25. The service bus DLL file is version 1.7.0.0. The client-side code—it sends a string message to the service. In Listing 8-26, a service interface named IEchoContract and a channel interface named IEchoChannel are defined. The message is sent via the created channel.

LISTING 8-25 Client-side configuration file

```
<xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.serviceModel>
    <client>
      <endpoint name="RelayEndpoint" contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTpcRelayBinding" />
    </client>
    <extensions>
      <bindingExtensions>
        <add name="netTpcRelayBinding" type="Microsoft.ServiceBus.Configuration.NetTpcRelayBindingCollectionElement, Microsoft.ServiceBus, Version=1.7.0.0, Culture=neutral, PublicKey=31bf3856ad364356" />
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

522 PART III Real-World Applications