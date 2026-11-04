For compilable languages, the client machine does essentially the same thing no matter which platform it's on (Java or Basic or PHP or Ruby): At compile time, it reads the WSDL and creates a proxy that the client talks to. This:

+   ♦ Brokers the communication process between the client and the service
+   ♦ Provides type safety, if it's supported
+   ♦ Generally makes your life easier because WSDL (and the contract it provides) is an important part of a service developer's work

![](bbox=[0.12, 0.38, 0.22, 0.55])

The contract isn't legally binding (and contains only a small amount of fine print). The service provider reserves the right to change the service any time it wants, and can even forgo updating the WSDL with no fear of legal reprisal. Because you're a .NET developer, though, your WSDL is generated automatically.

# *Chunky versus chatty*

Although the chunky-versus-chatty services issue might sound like a face-off between candy bars, it isn't.

Rather than perform small, incremental operations via Web services, you use them to make large, sweeping "strokes." The length of individual calls might be larger, but the number of communications is fewer, which reduces network overhead.

Suppose that an application changes the settings of a piece of hardware located miles away from it — perhaps your home heating system (which is a good use of a service). The client application (your computer) is absolutely local, the remote device (your heater) is certainly remote, and a network (probably the Internet) is in the middle. If you have a service with a series of individual controls, such as TurnFanOn and TurnFanOff, it's a common interface for a local application, such as connecting a heater directly to your computer.

The following chunk of code gives an example of that chatty sort of interface:

```
namespace HomeHeater
{
    public class Chatty : IChatty
    {
        public bool TurnFanOn()
        {
            return true;
        }
        public bool TurnFanOff()
        {
            return true;
        }
    }
}
```