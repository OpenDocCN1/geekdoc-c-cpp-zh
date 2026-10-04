# Making an ASMX Service 755

In the Java world, 10MB SOAP messages are not uncommon — although that includes the payload — and that works out to, 200,000 lines? In one HTTP call? That's probably a bit much.

SOAP dramatically increases your overhead in communication. If you don't need the security, federation, and transaction capabilities of SOAP, consider REST — covered in Chapter 4. If you're communicating in a homogenous environment, consider binary encoding.

On the other hand, if you're communicating in moderately heterogeneous environments and in fact need an encrypted, federated transaction using a common enterprise data model, by all means look at SOAP.

# Making an ASMX Service

You can write a SOAP service in ASMX or WCF.

ASMX doesn't stand for anything — it is ASPX with the $P$ changed to an $M$, which means Service. (Try not to laugh.) It is the extension of the ASP.NET web file that provides a service to a web page.

The thing is, ASMX allows only for SOAP. WCF does other things. I cover ASMX, I leave ASMX here because WCF's additional functionality makes WCF a clearer winner in this race. (For writing in WCF, check out Chapter 3.)

Book VII Chapter 2 Building Web Services with ASMX

Nonetheless, if you're making a publicly consumable service and need it to be straightforward and simple to deploy, then ASMX might be for you. Certainly, there is a lot of ASMX service code that you might have to maintain.

You can start by building one.

# Creating a new service

ASMX services are part of ASP.NET website projects. As such, they seem like a lot ASP.NET web applications — because they are ASP.NET applications. You can actually put an ASMX file in a regular ASP.NET application, and a web file in a service application like we do in the following step list. The template is there to help you get started.

+   1. Open Visual Studio and click New Project.
The New Project dialog box appears.
2. In Installed Templates under the Visual C# node, select Web.
3. In the box to the right, click ASP.NET Empty Web Application.