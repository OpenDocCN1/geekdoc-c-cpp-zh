```
```xml
host
    endpoint address="net.tcp://10.34.34.241/ChatServer"
        binding="netTcpBinding"
            bindingConfiguration="TcpConfig"
            contract="System.ServiceModel.PeerResolvers.
    IPeerResolverContract"
        endpoint
    service
services

bindings
    netTcpBinding
        binding name="TcpConfig"
            security mode="None"/>
        binding
    netTcpBinding
bindings
system.serviceModel
</configuration>
```
```

+   - **Config** file is very simple. A .NET predefined service is used in this, System.ServiceModel.PeerResolvers.CustomPeerResolverService.

+   - The base address is provided for hosting the resolver service as shown. The important thing about the end point is that it uses, System.ServiceModel.PeerResolvers.IPeerResolverContract contract which is already available in the foundation. Here, TCP end point is used for the communication. Hence the endpoint is provided with TCP binding and it is configured it security mode as none. Now the server is ready for chat client. Just start the server.

# 3. Chat Client

As compared to the Chat server, the client becomes little bit complicated. It does everything on its own. It needs something common that the server will use to communicate with clients and that can be established using interfaces.

The client code is as below.

```
```csharp
<CODE>
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Text;
using System.Windows.Forms;
using System.ServiceModel;
using System.ServiceModel.Channels;
```
```