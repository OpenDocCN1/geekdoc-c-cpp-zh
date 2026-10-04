
## Deploying

If you use IIS to host the service, deployment of WCF is the same as ASMX. You can effectively copy the .svc and .config files with the compiled binaries and have a working web application.

The better way to deploy in Visual Studio 2012 is to use the Publish Web. If you right-click the project and choose Publish, you have the option to set up a repeatable profile so that you don't forget anything (see Figure 3-8).

![](img/6df7bb88e9302e98442acc219cfbd7fc_802_0.png)

**Figure 3-8:** The Publish Web dialog box.

Book VII
Chapter 3

This panel does all the things that you would have to do yourself:

- Set the URL of the service
- Name the Application (in the site properties in IIS)
- Set up credentials
- Copy the right files

You can set up the profile once and reuse it every time you have to republish the application. Pretty slick.

## Consuming

All there is left to do is use it.

As one would expect, setting up a service reference for a WCF service is a lot setting up a reference for an ASMX service in Chapter 2 of this minibook. You should right-click and choose Add Service Reference, so you will get the dialog box shown in Figure 3-9, and you still can reference the service easily in your code.

Building Web with WCF

## 778 Creating a WCF Service

![](img/6df7bb88e9302e98442acc219cfbd7fc_803_0.png)

Figure 3-9: Adding the WCF service reference.

Two things to remember:

- The file extension you're looking for is .SVC.
- The binding you set up is abstracted away from you — one less thing you have to worry about.

Finding the file isn't a big deal, but the binding is important. Keep in mind that selecting a binding is invisible to the developer, but it has a significant impact on functionality and especially performance. The decision of which to use is not to be made lightly; it should be done only after much research and analysis.

## Chapter 4: Building Web Services with REST

In This Chapter

- Exploring the principles of REST
- Implementing REST services using WCF
- Consuming REST services

Chapter 3 includes a sidebar, "Using Different Endpoints," that has a big list of binding formats you can use with WCF. I point out that for instance, for most applications, you use SOAP, or binary. That's not necessarily accurate.

Another binding is pretty popular — it is the binding that your web browser uses to get pages from web servers. It is called REST, and it stands for Representational State Transfer.

In this chapter, I introduce you to REST and guide you through its advantages and drawbacks.

## Getting to Know REST

REST is basically the use of the traditional GET and POST patterns the old folks will remember from CGI. For your young pups, it is the basic format of web requests. For instance, when you click a link that looks like this:

```
http://mydomain.com/start.aspx?id=3
```

you’re using REST. Remember, we aren't talking about an implementation here. We are talking about a remote procedure call mechanism. It is just a way to get parameters for a query to a remote machine and to get data back.

We also aren't talking about a protocol, like SOAP. REST is an architecture. It has guidelines, not rules.

## Understanding the Guiding Principles of REST

A REST interface has four goals:

- Scalability of component interactions
- Generality of interfaces
- Independent deployment of components
- Intermediary components to reduce latency, enforce security, and encapsulate legacy systems

Use of REST with Windows Communication Foundation (WCF) meets most, but not all, of those goals. This chapter takes a quick look over the details of the implementation of REST in WCF, and you can make your own call.

## Understanding the Guiding Principles of REST

There are four guiding principles to REST. According to the standard, all RESTful interfaces provide interfaces that adhere to these principles. In the real world, compliance is up for discussion. Here are the principles:

- Identification of resources: individual resources (like a data item, for instance) are identified in requests (for example, using URIs in web-based REST systems). The resources themselves are conceptually separate from the database that are returned to the client. For example, the server doesn't send its database records expressed, but rather, as HTML, XML, or JSON that represents some database records expressed for instance, in French and encoded in UTF-8, depending on the details of the request and the server implementation.

- Manipulation of resources through these representations: When a client holds a representation of a resource, including any metadata attached, it has enough information to modify or delete the resource on the server, it has permission to do so.

- Self-descriptive messages: Each message includes enough information to describe how to process the message (for example, which parser to invoke). An example of this is the use of Internet media types, previously using MIME types. From the media type, the client must know how to process its contents. If it needs to look inside the message's contents in order to understand them, the message is not self-descriptive. For example, merely using the “application/xml” media type is not sufficient for knowing what to do with its contents.

- Hypermedia as engine: If the client will want to access (img/6df7bb88e9302e98442acc219cfbd7fc_805_0.png)

## Diving into REST

There are four guiding principles to REST. According to the standard, all RESTful interfaces provide interfaces that adhere to these principles. In the real world, compliance is up for discussion. Here are the principles:

- Identification of resources: individual resources (like a data item, for instance) are identified in requests (for example, using URIs in web-based REST systems). The resources themselves are conceptually separate from the database that are returned to the client. For example, the server doesn't send its database records expressed, but rather, as HTML, XML, or JSON that represents some database records expressed for instance, in French and encoded in UTF-8, depending on the details of the request and the server implementation.

- Manipulation of resources through these representations: When a client holds a representation of a resource, including any metadata attached, it has enough information to modify or delete the resource on the server, it has permission to do so.

- Self-descriptive messages: Each message includes enough information to describe how to process the message (for example, which parser to invoke). An example of this is the use of Internet media types, previously using MIME types. From the media type, the client must know how to process its contents. If it needs to look inside the message's contents in order to understand them, the message is not self-descriptive. For example, merely using the “application/xml” media type is not sufficient for knowing what to do with its contents.

- Hypermedia as engine: If the client will want to access

## 782 Setting up a WCF Service to REST

## Setting up a WCF Service to REST

The WCF services model is designed for SOAP but can use REST without a problem. Fortunately, in an update to .NET, Microsoft made a template for REST services. This template greatly simplifies the process of building cross-platform REST services.

Unfortunately, as of this writing, this template is only available for Visual Studio 2010. I assume that by the time you read this book, it will be available to use some C# 4.0 code to explain what will work in C# 5.0. It isn't optimal, I think the template is so powerful that it needs to be in the book.

![](img/6df7bb88e9302e98442acc219cfbd7fc_807_0.png)

## Getting the template

You should be able to go to the New Project dialog, click Online, and search for WCF REST in the dialog's Search box, and have the template appear. You can see it in Figure 4-1, it ain't there now.

![](img/6df7bb88e9302e98442acc219cfbd7fc_807_1.png)

If it were there, you would click it and install it. You have to approve a license agreement, and then you are good to go. Visual Studio manages any updates to the template from then.

If you have to be working in Visual Studio 2010, you can get the template from the Visual Studio Gallery. The full URL is http://visualstudiogallery.msn.microsoft.com/fbc7e5c1-a0d2-41bd-9d7b-e54c845394cd, but I imagine it is easier to go to http://visualstudiogallery.msn.microsoft.com and search for WCF REST.

![](img/6df7bb88e9302e98442acc219cfbd7fc_807_2.png)

| Book VII | Chapter 4 | Building Web Services with REST |
