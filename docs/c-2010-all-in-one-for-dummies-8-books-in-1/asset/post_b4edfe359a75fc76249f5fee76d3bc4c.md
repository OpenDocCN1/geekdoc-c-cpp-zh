
## 722 Understanding Web Services

```cs
AddStuffReference.ServiceSoapClient client = new
AddStuffReference.ServiceSoapClient();
client.AddStuffCompleted += new
EventHandler(client.AddStuffCompleted);
client.AddStuffAsynch("This is the stuff");
//This method is called when the response comes back.
//No timers or anything. .NET handles it for you.
void proxy_AddStuffcompleted(object sender, AddStuffReference.ServiceSoapClient
AddStuffcompletedEventArgs e)
{
    	bool result = e.Result.ToString();
}
```

The example below protects your user interface from experiencing a tie-up. You still have no indication that the messages will ever be delivered, so you should never write software that depends on the delivery of the data from the source. It has to fail gracefully.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_747_0.png)

## Contract driven

In client-server development, an interface defines a contract of sorts between the domain model and the user interface. That contract can be used to drive development in the same way as a contract is used to drive a business deal. If you know what I require and I know what you require, we quickly and easily make a deal.

A web service is required to have an interface that conforms to the Web Services Description Language (WSDL) standard. WSDL describes expected inputs and outputs as an interface, creating a contract between the service provider and the client.

In .NET, your contract is created automatically from the code for the service. If you call a service in the browser (which isn't the way it's designed to be called — I tell you more about that topic in minibook) from the development machine, you see the text screen shown in Figure I-1. Even though the browser gains some important information about the service, it is not the contract. The contract is shown behind the Service link.

Clicking the Service Description link appends the ?WSDL to the URL, and the Web browser shows the contract. This contract is used by the client system to determine exactly what information the service wants and how it will respond to input. The WSDL is displayed in a browser, as the interesting part is the XML that's behind the screen.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_748_0.png)

## WebService1

The following operations are supported. For a formal definition, please review the Service Description.

- HelloWorldService

This web service is using http://temp.org/ as its default namespace. Web service is mode public.

**Recommendation: Change the default namespace before publishing.** If you plan to call this web service from other services on the web, http://temp.org/ is available for WSDL services, but published WSDL services should use a more permanent name.

When you create your WSDL, you should use a unique domain name as the default namespace. Many WSDL namespaces, like URIs, do not need to point to actual resources on the Web. WSDL service namespaces are unique by design.

For XML services using WSDL, the default namespace can be changed using the WSDL attribute's namespace property. The Web service below is an example of code that sets the namespace to "http://microsoft.com/webservice/"

```xml
<WebService namespace="http://microsoft.com/webservice/">
    public class HelloWorld {
        implementation
    }
</>
```

**Figure 1-1:
The default service overview.**

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_748_1.png)

## Book VII
Chapter 1

Getting Acquired with Web Services

**Figure 1-2:
The Service Description in WSDL.**

For compilable languages, the client machine does essentially the same no matter what platform it's on (Java or Basic or PHP or Ruby): At compile time, it reads the WSDL and creates a proxy that the client talks to:

- Brokers the communication process between the client and the service
- Provides type safety, if it's supported
- Generally makes your life easier because WSDL (and the contract it provides) is an important part of a developer's work

The contract isn't legally binding (and contains only a small amount of fine print). The service provider reserves the right to change the service it waits for, and can even forgo updating the WSDL with no fear of legal reprisal. You're a .NET developer, though, your WSDL is generated automatically.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_749_0.png)

## Chunky versus chatty

Although the chunky-versus-chatty services issue sound like a face-off between candy bars, it isn't.

Rather than perform small, incremental operations over Web services, we use them to make large, sweeping "strokes." The length of individual calls might be larger, but the number of communications is fewer, which reduces network overhead.

Suppose that an application changes the settings of a piece of hardware miles away from it — perhaps your heating system (which is a good use of a service). The client application (your computer) is absolutely local, the remote device (your heater) is certainly remote, and a network (probably the Internet) is in the middle. If you have a service with a series of individual controls, such as TurnFanOff and TurnFanOff, it's a common interface for a local application, such as connecting a heater directly to your computer.

The following chunk of code gives an example of that chatty sort of interface:

```cs
namespace HomeHeater {
    public class Chatty : IChatty {
        public bool TurnFanOn() {
            return true;
        }
        public bool TurnFanOff() {
            return true;
        }
    }

public bool SetTemperature(int newTemperature)
{
    return true;
}
public bool SetFanSpeed(string newFanSpeed)
{
    return true;
}
```

The interface in this example is chatty (in case you couldn't tell from its class name). Every time you change a knob on the controller, a call is made to a service. Move the temperature to 72 degrees and call the service. Turn the fan to its High setting and call the service. Turn the temperature back down and call the service. The client "chats" with the service.

Nothing is intrinsically wrong with this implementation. For a service, though, with more network overhead for every call, it is not the best way to build methods. Instead, want your client to change settings and then pull a lever on the side to make all the changes at one time.

A chatty interface provides a domain model for the client to use, with properties to set. After all settings are in the model object, send the whole shootin match to the service. It looks like this:

```cs
namespace HomeCenter{
    public class Chunky : IChunky{
        public bool UpdateHeaterSettings(HeaterModule heaterModule)
        {
            return true;
        }
        public class HeaterModule{
            public int Temperature { get; set; }
            public bool FanOn { get; set; }
            public string FanSpeed { get; set; }
        }
    }
```

No, no matter how often you make changes, the service is called only when you "pull the big lever" (update it). This action prevents users from updating after every change depends on your interface. In general, this design principle is the best for service development.

You may wonder why anyone would bother with a concept as convoluted as Web services. I can assure that good reasons exist and that you will want to use this technology on a project.

## Building Service-Oriented Applications

The first and most obvious use of a service is to create a Service-Oriented Application, or SOA. This overloaded, term means that your application (like the heating system I mentioned in the previous section) uses services to assist a remote client with communications with a server.

Unfortunately, the term SOA is no longer useful in the marketplace. So many so-called "experts" have chimed in with large, unmanageable ideas for the creation of systemwise services that it is impossible for anyone to separate the wheat from the chaff.

The concept is simple: The user interface calls a service at some point in the process to communicate with the server. You do this for two reasons:

- Scalability: It's the main reason to use a service inside an application — especially a Web Application.

Up to a point, most Web Applications have built-in scaling. If you need more access points, you just add more servers and use a device to sort the traffic to another machine, as shown in Figure 1-3.

Web applications are different, though, because layers have different scalability needs. Sometimes the database is loaded, and sometimes the Web server is. You must be able to separate the layers of the application, as shown in Figure 1-4 — that's where services start to become useful.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_751_0.png)

Figure 1-3: Scaling on a simple Web site.
