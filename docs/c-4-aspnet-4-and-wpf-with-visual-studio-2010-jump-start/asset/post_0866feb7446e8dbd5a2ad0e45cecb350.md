
## Is This Web Forms 4.0?

One of the major concerns that we’ve heard when talking to people about ASP.NET MVC is that its release means the death of Web forms. This just isn’t true. ASP.NET MVC is not ASP.NET Web forms 4.0. It’s an alternative to Web forms, and it’s a fully supported part of the framework. While Web forms continues to march on with new innovations and new developments, ASP.NET MVC will continue as a parallel alternative that’s totally supported by Microsoft.

One interesting way to look at this is to refer to the namespaces these technologies live in. If you could point to a namespace and say, “That’s where ASP.NET lives,” it would be the `System.Web` namespace. ASP.NET MVC lives in the `System.Web.Mvc` namespace. It’s not `System.Mvc`, and it’s not `System.Web2`.

Although ASP.NET MVC is a separately downloadable Web component today for users of Visual Studio 2008 (often referred to by the ASP.NET team as an out-of-band [OOB] release), it has been folded into .NET Framework 4 and it’s built into Visual Studio 2010 out of the box. This cements ASP.NET MVC’s place as a fundamental part of ASP.NET itself.

## Why Not Web Forms?

In ASP.NET Web forms, you create an instance of `System.Web.UI.Page` and put “server controls” on it (for example, a calendar and some buttons) so that the user can enter or view information. You then wire these controls to events on the `System.Web.UI.Page` to allow for interactivity. This page is then compiled, and when it’s called by the ASP.NET runtime, a server-side control tree is created, each control in the tree goes through an event lifecycle, it renders itself, and the result is served back as HTML. As a result, a new Web aesthetic started to emerge — Web forms layers eventing and state management on top of HTTP — a truly stateless protocol.

Why was this abstraction necessary? Remember that Web forms was introduced to a Microsoft development community that was very accustomed to Visual Basic 6. Developers using VB6 would drag buttons onto the design surface, double-click the button, and a `Button_Click` event handler method was instantly created for them. This was an incredibly powerful way to create business applications and had everyone excited about Rapid Application Development (RAD) tools. When developers started using classic ASP, it was quite a step backward from the rich environment they were used to in Visual Basic. For better or worse, Web forms brought that Rapid Application Development experience to the Web.

However, as the Web matured and more and more people came to terms with their own understanding of HTML as well as the introduction of CSS (Cascading Style Sheets) and XHTML, a new Web aesthetic started to emerge. Web forms is still incredibly productive for developers, enabling them to create a Web-based line of business applications very quickly. However, the HTML it generates looks, well, generated and can sometimes offend the sensibilities of those who handcraft their XHTML and CSS sites. Web forms concepts like ViewState and the Postback event model have their place, but many developers want a lower-level alternative that embraces not only HTML, but also HTTP itself.

Additionally, the architecture of Web forms also makes testing via the current unit testing tools such as NUnit, MbUnit, and xUnit.NET difficult. ASP.NET Web forms wasn’t designed with unit testing in mind, and although a number of hacks can be found on the Web, it’s fair to say that Web forms does not lend itself well to test-driven development. ASP.NET MVC offers absolute control over HTML, doesn’t deny the existence of HTTP, and was designed from the ground up with an eye towards testability.

## ASP.NET MVC Is Totally Different!

Yes, ASP.NET MVC is totally different. That’s the whole point. It’s built on top of a system of values and architectural principles that is very different from those in Web forms. ASP.NET MVC values extensibility, testability, and flexibility. It’s very lightweight and doesn’t make a lot of assumptions on how you will use it — aside from the fact that it assumes you appreciate the Model-View-Controller pattern.

Different developers and different projects have different needs. If ASP.NET MVC meets your needs, use it. If it doesn’t, don’t use it. Either way, don’t be afraid.

## Why “(ASP.NET > ASP.NET MVC) == True”

Creating your first MVC application is fairly straightforward. You can use any version of Visual Studio 2010 to create the basic application, including Express, Standard, Professional, or Team Edition.

If you’re NOT using Visual Studio 2010, the first order of business is to install the MVC Framework on your 2008 development box. Start at www.asp.net/mvc by downloading the latest release. If you like living on the edge, you can often get ASP.NET MVC future releases at www.codeplex.com/aspnet.

What you’re downloading is a set of Visual Studio project templates that will create your ASP.NET MVC Web application for you. You’ve used these before — every new ASP.NET Web site and ASP.NET Web application is based on a set of templates. The templates will be installed in Visual Studio, and the reference assemblies will be installed in C:\Program Files\Microsoft ASP.NET.

After you’ve installed ASP.NET MVC, you’re ready to create an ASP.NET MVC application using Visual Studio 2008. Though, if you are using Visual Studio 2010, then you are going to want to follow these steps:

- 1. Open Visual Studio 2010 by selecting File -> New Project.
- 2. From the New Project dialog box, shown in the next figure, select ASP.NET MVC 2 Web Application.

![](img/7954dcc7dd1d929d072aec8e9531b6cc_58_0.png)

Another outstanding feature found in this release of the .NET Framework is the WCF Data Services framework. This feature enables you to easily create a cloud interface to your client applications that provides everything from simple read capabilities to a full CRUD model (create, read, update, and delete functions). This feature was previously referred to as ADO.NET Data Services.

When you are working with ASP.NET, there is now a lot more focus on putting work down on the client as well as the server. In the past, much of the development focused on performing as much on the server as possible and delivering completed operations and UI back down to the client simply for viewing. With the release of “smart clients” and AJAX-enabled applications, much of the work is now being offloaded to the client. WCF Data Services makes exposing back-end capabilities over the wire to enable more work to be performed on the client even easier than before.

WCF Data Services works to create a services layer to your back-end data source. Doing so yourself, especially if you are working with a full CRUD model, means a lot of work. WCF Data Services allow you to get a service layer that is URI-driven. The following figure shows the general architecture when you’re working with WCF Data Services.

![](img/7954dcc7dd1d929d072aec8e9531b6cc_60_0.png)

As you can see from this figure, the WCF Data Services layer is not the layer that interacts with the database. Instead, you are working with an EDM layer that is the mapping layer between the data store and the cloud-based interface. When working with your EDM, you are able to use LINQ to SQL and LINQ to Entities.

WCF Data Services allow you to quickly expose interactions with the application’s underlying data source as RESTful-based services. The current version of WCF Data Services allows you to work with the datastores using JSON or Atom-based XML. Again, JSON is what ASP.NET AJAX uses for doing out-of-bounds calls to get around doing a complete page refresh.

## CREATING YOUR FIRST SERVICE

Figuring out how to build a complete services layer to your database for all create, read, update, and delete functions would take some serious time and thought. However, WCF Data Services makes this task much more feasible, as you will see as you work through this first example.

To build a services layer, first create a standard ASP.NET Web Application called Web_ADONETDS in either Visual Basic or C#. Note, you need to use the .NET Framework 3.5 SP1 along with Visual Studio 2008 SP1 or the .NET Framework 4 with Visual Studio 2010 for this example to work.

This, of course, creates a standard Web application that is not different from normal. Because WCF Data Services works from an underlying database, you will need to add one. For this example, add the NORTHWND.mdf database. Place this database within the App_Data folder of your project.

### Adding Your Entity Data Model

After you have the database in place, you next create an Entity Data Model that WCF Data Services will work with. To do this, right-click on your project and select Add ⇨ New Item from the list of options in the provided menu.

The Add New Item dialog appears. As illustrated here, add an ADO.NET Entity Data Model to your project.

![](img/7954dcc7dd1d929d072aec8e9531b6cc_61_0.png)

As shown in the figure, name your ADO.NET Entity Data Model file Northwind.edmx. When you create the Northwind.edmx file by clicking Add, the Entity Data Model Wizard appears, offering you the option of creating an empty EDM or creating one from a pre-existing database. For this example, choose the option to create one from the pre-existing (Northwind) database. Then click Next in the wizard.
