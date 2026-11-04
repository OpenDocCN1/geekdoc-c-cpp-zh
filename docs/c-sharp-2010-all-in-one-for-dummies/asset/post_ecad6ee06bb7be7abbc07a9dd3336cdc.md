
## Book VI
## Web Development with ASP.NET
### The 5th Wave
By Rich Tennant

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_652_0.png)

> "Okay, I think I forgot to mention this, but we now have a Web management function that automatically alerts us when there's a broken link on The Aquarium's Web site."

## Contents at a Glance
- Chapter 1: Looking at How ASP.NET Works with C# .........629
- Chapter 2: Building Web Applications .........641
- Chapter 3: Controlling Your Development Experience .........659
- Chapter 4: Leveraging the .NET Framework .........685
- Chapter 5: Digging into Web Construction .........703

## Chapter 1: Looking at How ASP.NET Works with C#
### In This Chapter
- ✓ Getting to know Web applications
- ✓ Conferring with the client
- ✓ Working with Web servers

When I first started writing about World Wide Web applications, I had to describe the Web first. There were still a significant number of programmers who didn't know what it was, or thought it was CompuServe.

I don't really have that problem anymore.

The World Wide Web is now ubiquitous. Programmers of all stripes use the Web for research and communication. Providers use it for product updates and documentation. It is everywhere.

All the more reason to know how to code in the Web environment. Problem is that there are so many so-called frameworks for development that it is nearly impossible to decide which to use with a reasonable methodology. You almost have to draw straws.

If you are working in a Microsoft environment, and if you are writing a non-exceptional program, I recommend that you use plain, vanilla ASP.NET. Why? Sempf's Fourth Law: Simplicity above all. ASP.NET is a straightforward platform for Web creation.

ASP.NET has its share of problems, most of which involve writing Google (or some other really big complicated program). You probably aren't writing Google, so don't worry about it. If your site gets famous, you can get some venture capital and rewrite it into some custom framework. For now, just get your site written. That's what ASP.NET enables you to do — get the job done. With ASP.NET, you can write a good Web site quickly, one that can be hosted just about anywhere. No one can ask for much more than that. This chapter delves into the details of using ASP.NET with C#.

## Breaking Down Web Applications

A Web application is a computer program that uses a very light client interface communicating with a server over the Internet in a stateless manner. Stateless means that the computer browsing the site and the server providing the site don't maintain a connection. You can see this process at a high level in Figure 1-1.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_655_0.png)

Figure 1-1:
The Web application process.

The client requests a document from the server, and the server sends the document when it gets around to it. The document, usually a combination of Hypertext Markup Language (HTML), Cascading Style Sheets (CSS), and JavaScript, contains standardized elements which make up the interface of the application.

Why do we need this? If there is just a set of documents on the server and the client is just requesting one after another, what's the point of that? Of course, getting a document is a good thing, but where does the application part come in?

The answer is within Web applications. Web applications are powerful because the server can construct the document on the fly whenever it receives a request. This server process is what makes Web applications work. (See Figure 1-2.)

Don't get me wrong, the light client interface — called the Web browser or just the browser — provides some important functionality. It handles the user interface and can do things independently of the server.

The server is largely where it's at, though. Because the server can remember things from moment to moment, and because it is assumed that the client forgets everything from page to page, the server is where the long-running communications all reside.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_656_0.png)

Figure 1-2: ASP.NET deconstructed.

ASP.NET is a library of controls and processing logic that makes constructing the server side of things much easier. You construct "server pages," but they end up transformed into the documents that the client uses to show you the user interface. ASP.NET is classified as a Web Application Framework, not a programming language.

The programming language, for our purposes, is C#. However, you can code for ASP.NET in any .NET language — it is just another set of tools in the framework.

C# is the language that you use to tell the server how to organize the ASP.NET pieces and send them to the client. The clients will never see any C# code; they won't even know that you coded it in C#.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_657_0.png)

This gets into the same discussion that we have several times throughout the book regarding the difference between the library and the language. ASP.NET is a library of tools, and that library is language independent. You orchestrate the functionality of the parts of the library using the language.

There are a few little caveats to Web development, however. The client — which doesn't care a whit that you are coding in C# — needs some care and feeding. There is no state in Web applications, so you need to think a little differently. The client does a lot automatically for you in Web development. The server has some security concerns.

Before we dig into the details of using C# with ASP.NET, I'd like to take a tour through the details of Web development and point out some things you need to keep in mind. So here we go.

## Questioning the Client

When you are writing a Windows Form, WPF, or console application, your platform for the client is a Windows computer. When you are writing a Web application, you have no idea what the platform for your client is. It could be a Mac, any one of 12 Windows operating systems, or Linux. It could be a phone, a tablet, or a netbook. It could be a television, a gaming device, or a refrigerator (really: see Figure 1-3).

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_657_1.png)

Figure 1-3: Yes, a refrigerator.

The point is that you don't know what you are writing for, so you have a very different development experience for a Web browser than you do for a Windows client. You don't know what size the screen is, you don't know what language the machine is set to, you don't know how fast the connection to the Internet is. You know nothing about your client.

You have to question the client. You can't assume much about the browser, so you have to make certain design decisions differently than you usually would.

You can depend on the browser to do some things for you that you might be used to having to do for yourself. The programming details are explained in Chapter 4, but it is important to get a good overview now.

First, the client browser has a built-in scripting system called ECMAScript. Second, the browser can tell you some subset of details about itself, its host machine, and the user that is using it.

### Scripting the client

By now you get the idea that communication with the browser occurs via the network, and that the client and browser are disconnected. Although that is true, the client isn't completely out in the fog when it comes to interacting with the user.

You can send a script along with your HTML document. This script references objects on the screen — just like your C# code would — and makes things happen for the user.

Usually this script is in the JavaScript language. Why not C#? Well, C# isn't a scripting language. C# needs to be compiled, and JavaScript isn't compiled. It just sits there, in text, waiting for the browser to run it.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_658_0.png)

The fact that it is in text means you have to be careful not to put secure information in a script. Right-click on any Web page in your browser and click View Source to see that page's script code.

A lot of the script that your pages need will be generated by ASP.NET. This book is about C#, not JavaScript, so we will focus on the server features, not the client features. For now, you should just know that "things are happening" on the client side, however.

### Getting information back from the client

When a browser makes a request to a server, a lot of useful information about the client gets sent along with the page name that is requested. You can reference this in the backwardly named ServerVariables collection.

This is about as good as learning about the client gets. These details will, however, help you get the most out of your communication with the client. Here some examples of the values available:

- AUTH_USER: The logged-in user.
- REMOTE_USER: The same as AUTH_USER.
