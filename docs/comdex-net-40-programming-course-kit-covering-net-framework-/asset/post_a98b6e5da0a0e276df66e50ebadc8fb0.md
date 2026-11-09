
```aspx
<asp:GridView BackColor="#FFFFFF" ForeColor="#330099"
              HorizontalAlign="Center" />
<RowStyle BackColor="White" ForeColor="#330099" />
<SelectedRowStyle BackColor="#F6FCC6" Font-Bold="True" ForeColor="#663399" />
<SortedAscendingCellStyle BackColor="#FFEFBE" />
<SortedAscendingHeaderStyle BackColor="#AF0101" />
<SortedDescendingCellStyle BackColor="#F6F0C0" />
<SortedDescendingHeaderStyle BackColor="#7E0000" />
</asp:GridView>
```

In the preceding listing, we have added the GridView control to the Default.aspx page.

- 22. Write the code, shown in Listing 10.8, in the code-behind file of the **Default.aspx** file (**Default.aspx.cs** file):

### Listing 10.8: Code for the Default.aspx.cs File

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using ServiceReference1;
public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        NORTHWNDEntities svc = new NORTHWNDEntities(new
            Uri("http://localhost:9368/DataService/WcfDataService.svc/"));
        GridView1.DataSource = svc.Customers;
        GridView1.DataBind();
    }
}
```

In the preceding listing, the NORTHWND database is bound to the **GridView** control through the URL of **WcfDataService.svc** data service.

- 23. Press the F5 key to run the application. The output is shown in Fig. ASP-10.42:

![](img/9862a98a1a2d3bb14334137965a1ec60_693_0.png)

Fig. ASP-10.42

Let’s now summarize the main topics discussed in this chapter.

### Summary

In this chapter, you have learned to create the Web and WCF services. You have also learned how to use these services in client applications with ASP.NET 4.0. Next, the chapter discussed about the new WCF Data Service feature and how to create WCF Data Services.

In the next chapter, you will learn about Silverlight 4.0 that is used to create rich interactive Web applications.

## Introducing Silverlight 4.0

### CHAPTER 11

### In this Chapter:

- Exploring Key Features of Silverlight
- Exploring New Features of Silverlight 4.0
- Explaining the Silverlight Architecture
- Installing Silverlight 4.0 Tools
- Assemblies and Files in Silverlight Applications
- Controls Used in Silverlight Applications
- Developing Silverlight Applications

In the initial years of Web development, **HyperText Markup Language (HTML)** was used to create Web sites. The content in the Web pages of these Web sites was predominantly static. As time progressed, new scripting languages, such as **Extensible HyperText Markup Language (XHTML)** and JavaScript, and technologies, such as Cascading Style Sheets (CSS) and Adobe Flash, were introduced. These new languages and technologies helped Web developers to create interactive Web sites. However, some of these technologies were expensive to deploy on the Web server and their performance on different platforms also varies. To address these problems, Microsoft introduced **Silverlight**.

Silverlight is a technology used to create Web sites that can have high-resolution multimedia content and eye-catching visual effects, which in turn provide an attractive look and feel to your Web site. It is shipped with .NET Framework and compatible with multiple browsers, devices and operating systems; thereby, allowing you to make interactive websites.

The first version of Silverlight released by Microsoft was Silverlight 1.0. This version, released in 2007, was based on the JavaScript application model. In October 2008, an upgrade to Silverlight 1.0, called Silverlight 2.0 was released, which is supported by Visual Studio 2008 Service Pack 1 (SP1). After that, an upgrade to Silverlight 2.0 was released, named as Silverlight 3.0, which is supported by Visual Studio 2010. The latest version of Silverlight is Silverlight 4.0, which is also fully supported by Visual Studio 2010.

In this chapter, you learn about the various features of Silverlight including the new features introduced in Silverlight 4.0. Next, you learn about the architecture of Silverlight 4.0. Further, you learn how to install Silverlight 4.0 Tools on your system. You also learn about different controls available in Silverlight 4.0. Finally, you learn to develop applications in Silverlight using the new controls.

Let’s start by discussing the key features of Silverlight.

### Exploring Key Features of Silverlight

Silverlight, previously known as WPF/E, is a subset of Windows Presentation Foundation (WPF) and inherits many functionalities of WPF. For example, Silverlight supports Extensible Application Markup Language (XAML), two-dimensional (2D) vector graphics, animations, and multimedia. Silverlight applications can run in multiple Web browsers. Silverlight offers a variety of features that facilitate Web developers and designers to build interactive websites. The main features of Silverlight are as follows:

- Supported by .NET programming model
- Comprehensive User Interface (UI) Framework
- Support for the Deep Zoom technology
- Support for three-dimensional (3D) graphics, animations, and multimedia
- Support for networking
- Support for higher quality video and audio
- Out-of-Browser capabilities

Now, let’s discuss each of these features in detail.

### Supported by .NET Programming Model

Silverlight is supported by the .NET Framework programming model and also inherits features, such as type-safety and exception handling, from .NET Framework. Therefore, you can use any .NET language, such as Visual Basic and C#, to develop Silverlight applications with ease. It also includes many classes from the base class library of .NET Framework that enable you to work with Input/Output (I/O) operations, collections, and generics. Silverlight also supports Language Integrated Query (LINQ), which enables you to work with the various types of data sources, such as Structured Query Language (SQL) databases and Extensible Markup Language (XML) files in the Web sites.

### Comprehensive UI Framework

Silverlight has a comprehensive UI Framework that contains predefined controls, layout, styles, themes, and templates that help you build interactive Web sites as well as attractive Web sites. In case the existing set of controls and styles do not meet your requirements, you can also use custom styles and control templates in Silverlight applications. This in turn helps you to make your Web site more user-friendly. The data-binding and data-manipulation controls, such as **DataGrid**, can also be used in Silverlight Web site to retrieve and store data in databases.

### Support for Deep Zoom Technology

Silverlight includes a support for a technology called Deep Zoom, which allows you to zoom high-resolution images in Web sites. With the help of the Deep Zoom technology, you can easily zoom in or out multiple images simultaneously. This technology reduces the time required for initial load by downloading only the region being viewed. It also allows you to view thousands of images simultaneously.

### Support for 3D Graphics, Animations, and Multimedia

Silverlight has built-in support for 2D vector graphics and animations. In addition, it allows you to create, transform, and animate 2D shapes. However, with the release of Silverlight 3.0, you can perform perspective 3D transformations to create more attractive Web visuals containing new 3D graphics, animation features, and hardware accelerated effects. Perspective transforms are transformations that you can apply on Extensible Application Markup Language (XAML) elements to simulate a 3D environment. You can apply 3D effects to controls in your Silverlight applications by using the attached property, called Projection, within a parent element. Consider the following code snippet:

```xml
<Button Height="90" Content="Perspective Transform">
<Button.Projection>
<PlaneProjection RotationY="60"/>
</Button.Projection>
</Button>
```

In the preceding code snippet, the Button control is rotated to give it a perspective, with a 60 degree rotation on the Y-axis.

In addition, you can make your Web sites dynamic by using storyboards and controlling the animation timeline and speed. For this, you can include .jpeg or .png extension images in the Web sites. Silverlight also supports various multimedia formats, such as .wma, .wmv, and .mp3, to play multimedia content on the Web site. You can also use High-Definition (HD) quality video (up to 720p) in Silverlight applications.

![](img/9862a98a1a2d3bb14334137965a1ec60_696_0.png)

> **Vector graphics are shapes and drawing used to represent geometrical images, such as points, lines, curves, and polygons.**

### Support for Networking

Silverlight contains classes to support networking and predefined sockets. It allows you to use various services, such as Hypertext Transfer Protocol (HTTP), XML, Really Simple Syndication (RSS), and Representational State Transfer (REST) to develop distributed applications. Silverlight extends the cross-domain support for networking to enable communication with a server.

### Support for Higher Quality Video and Audio

Silverlight supports the high quality video and audio. It supports new audio and video formats, such as H.264, Advanced Audio Coding (AAC), and Moving Picture Experts Group (MPEG) 4. In addition, it includes support for live and on-demand Internet Information Services (IIS) 7 Smooth Streaming, full HD (720+) playback, and raw audio or video (AV) pipeline. The raw AV pipeline enables the .NET developers to provide audio/video decoding that can be hosted outside the .NET Framework runtime environment.

### Out-of-Browser Capabilities

The Out-of-Browser capability, first introduced with the Silverlight 3.0, enables the Silverlight applications to run either within or outside a Web browser. It means that you can install a Silverlight
