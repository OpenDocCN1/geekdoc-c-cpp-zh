# Running Your Site under IIS | 75

+   1. Install and configure IIS.
2. Install and configure the .NET Framework 4.5.1.
3. Configure security settings.

Depending on the current state of your system, some of these actions are optional. In the following sections, see how to carry out these steps.

> NOTE Installing and configuring a web server can be a complex task. You have many factors to take into account, including your operating system, its configuration, the account you use to log on to your machine, the final SQL Server you're going to use, and more. Don't panic if you get stuck, visit the IIS website for detailed walkthroughs, or come over to this book's own discussion forum at http://piz.prox.com, where you will find programmers (me) that will help you succeed.

The steps described in the remainder of this chapter should work on Windows 7, Windows 8 and 8.1, Windows Server 2008 R2, and Windows Server 2012 / 2012 R2. For a more information about IIS, including help with installing IIS on older versions of Windows not discussed here, check out the official IIS website at www.iis.net.

# Installing and Configuring the Web Server

Although IIS has with most Windows versions, it's not installed by default, so you need to do that first. You also need to make sure your version of Windows supports IIS. Although the Starter and Home Basic versions of Windows 7 and 8 ship with some parts of IIS, you can't run ASP.NET pages on them, so you need at least the Home Premium Edition. On the server-based versions of Windows, IIS is fully supported. If you're hosting your site with an external hosting company, you can skip the following steps on installing IIS.

> NOTE Even though IIS is supported on consumer versions of Windows such as Windows 7 and 8, it doesn't mean these operating systems are the best choices for hosting your website. You typically use these versions of Windows for local development and testing, whereas the server versions of Windows (such as Windows Server 2008 R2 and Windows Server 2012 / 2012 R2) are used for hosting production websites.

To install and configure IIS on your Windows machine, you need to be logged on as an administrator. If the account you use to log on to your machine does not have administrative privileges, you need to ask your administrator to install and configure IIS for you.

In addition to installing IIS, you also see how to create and configure the website in IIS. Because of the way security works under Windows, your site probably won't work immediately after you configure