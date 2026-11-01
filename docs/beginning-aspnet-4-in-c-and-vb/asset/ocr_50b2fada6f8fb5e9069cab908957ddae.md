# Server

The server is implemented within a console application. With RemotingConfiguration.Configure(), the configuration file is read and thus the channel and remote objects are set up. With the Console.ReadLine() the server waits until the user stops the application:

```
```csharp
using System;
using System.Runtime.Remoting;
namespace Wrox.ProCSharp.Remoting
{
    class Server
    {
        static void Main()
        {
            RemotingConfiguration.Configure("Server.exe.config", true);
            Console.WriteLine("press return to exit");
            Console.ReadLine();
        }
    }
}
```
```

code snippet RemotingAndEvents/RemoteServer/Program.cs

# Server Configuration File

The server configuration file, Server.exe.config, is also created as already discussed. There is just one important point: the remote object must keep state for the client because the client at first registers the event handler and calls the remote method afterward. You cannot use single-call objects with events, so the RemoteObject class is configured as a client-activated type. Also, to support delegates, you have to enable full serialization by specifying the typeFilterLevel attribute with the <provider> element:

```
```xml
<configuration>
    <system.runtime.remoting>
        <application name="CallbackSample">
            <service>
                <activated type="Wrox.ProCSharp.Remoting.RemoteObject, RemoteObject" />
            </service>
            <channels>
                <channel ref="tcp" port="6791">
                    <serverProviders>
                        <provider ref="binary" typeFilterLevel="Full" />
                    </serverProviders>
                </channel>
            </channels>
        </application>
    </system.runtime.remoting>
</configuration>
```
```

code snippet RemotingAndEvents/RemoteServer/app.config

# Event Sink

An event sink library is required for use by the client and is invoked by the server. The event sink implements the handler StatusHandler() that's defined with the delegate. As previously noted, the method