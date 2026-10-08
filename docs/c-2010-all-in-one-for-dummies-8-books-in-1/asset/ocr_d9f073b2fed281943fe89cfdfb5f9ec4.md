# 632 Questioning the Client

This gets into the same discussion that we have several times throughout the book regarding the difference between the library and the language. ASP NET is a library of tools, and that library is language independent. You orchestrate the functionality of the parts of the library using the language.

There are a few little caveats to Web development, however. The client — which doesn't care what you are coding in C# — needs some care and feeding. There is no state in Web applications, so you need to think a little differently. The client does not automatically for you in Web development. The server has some security concerns.

Before we dig into the details of using C# with ASP.NET, I'd like to take a tour through the details of Web development and point out things you need to keep in mind. So here we go.

# Questioning the Client

When you are writing a Windows Form, WPF, or console application, your platform for the client is a Windows computer. When you are writing a Web application, you have no idea what the platform for your client is. It could be a Mac, any one of 12 Windows operating systems, or Linux. It could be a phone, a tablet, or a notebook. It could be a television, a gaming device, or a refrigerator (really: see Figure 1-3).

![](bbox=[0.152, 0.565, 0.478, 0.793])

The point is that you don't know what you are writing for, so you have a very different development experience for a Web browser than you do for a Windows client. You don't know what size the screen is, you don't know what language the machine is set to, you don't know how fast the connection to the Internet is. You know nothing about your client.