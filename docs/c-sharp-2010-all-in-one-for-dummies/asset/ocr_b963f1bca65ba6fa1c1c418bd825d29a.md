```
<myApp:EBDCCode> ... </myApp:EBDCCode>
<wsa:ReferenceParameters>
</wscoor:RegistrationService>
<myApp:IsolationLevel>
RepeatableRead
</myApp:IsolationLevel>
</wscoor:CoordinationContext>
```

In the Java world, 10MB SOAP messages are not uncommon — although that includes the payload — and that works out to what, 200,000 lines? In one HTTP call? That's probably a bit much.

SOAP dramatically increases your overhead in communication. If you don't need the security, federation, and transaction capabilities of SOAP, consider ReST — covered in Chapter 4. If you are communicating in a homogenous Microsoft environment, consider binary encoding.

On the other hand, if you are communicating in moderately heterogeneous environments and do in fact need an encrypted, federated transaction using a common enterprise data model, by all means look at SOAP.

# Making an ASMX Service

You can write a SOAP service in ASMX or WCF.

ASMX doesn't stand for anything — it is ASPX with the P changed to an M, which means Service. (Try not to laugh.) It is the extension of an ASP.NET Web file that provides a service rather than a Web page.

The thing is, ASMX allows only for SOAP. WCF does other things. Here I cover ASMX; I leave ASMX here because WCF's additional functionality makes WCF a clear winner in this race. (For writing in WCF, check out Chapter 3.)

Nonetheless, if you are making a publically consumable service and need it to be straightforward and simple to deploy, then ASMX might be for you. Certainly, there is a lot of ASMX service code out there which you might have to maintain.

Let's just start by building one.

# Creating a new service

ASMX Web services are ASP.NET projects. As such, they seem a lot like ASP.NET Web applications — because they are ASP.NET Web applications. You can actually put an ASMX file in a regular ASP.NET application, and a Web file in a Web service application like we do in the following step list. The template is just there to help you get started.