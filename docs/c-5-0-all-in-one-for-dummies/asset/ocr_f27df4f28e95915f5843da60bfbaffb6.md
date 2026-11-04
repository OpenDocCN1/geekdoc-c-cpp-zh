Clicking the Service Description link appends the text ?WSDL to the URI, and the web browser shows the contract. The client system used this contract to determine exactly which information the service wants and how it will respond to input. Though the WSDL is displayed in a browser, as shown in Figure 1-2, the interesting part is the XML that's behind the screen.

Figure 1-2:
The Service Description
in WSDL

![](bbox=[0.24, 0.33, 0.86, 0.71])

For compilable languages, the client machine does essentially the same thing no matter which platform it's on (Java or Basic or PHP or Ruby): At compile time, it reads the WSDL and creates a proxy that the client talks to. This

+   - Brokers the communication process between the client and the service
+   - Provides type safety, if it's supported
+   - Generally makes your life easier because WSDL (and the contract it provides) is an important part of a service developer's work

![](bbox=[0.14, 0.88, 0.22, 0.97])

The contract isn't legally binding (and contains only a small amount of fine print). The service provider reserves the right to change the service any time it wants, and can even forgo updating the WSDL with no fear of legal reprisal. Because you're a .NET developer, though, your WSDL is generated automatically.

# Chunky versus chatty

Although the chunky-versus-chatty services issue might sound like a face-off between candy bars, it isn't.