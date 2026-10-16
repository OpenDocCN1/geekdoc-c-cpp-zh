
![](img/3d365b72b289213a91ade7eb366b8f35_1759_0.png)

**Figure 45.11**

Later you can modify bindings to the IP address, port number, and hostname by clicking the Edit button in the Site Binding dialog (see Figure 45.12). You can also define other protocols such as `net.tcp` or `net.http` that can be used to host a Windows Communication Foundation (WCF) application. For this to be available, you need to install optional Windows features: WCF Services are available with the .NET Framework 4.6 Advanced Services in the Turn Windows Features On or Off management tool.

![](img/3d365b72b289213a91ade7eb366b8f35_1759_1.png)

**Figure 45.12**

> **NOTE** Read Chapter 44, “Windows Communication Foundation,” for more information about WCF.

## Creating an Application

Next, you can create an application. Figure 45.13 shows creating an application named ProCSharpApp within the site ProCSharpSite running within the application pool ProCSharpPool.

![](img/3d365b72b289213a91ade7eb366b8f35_1760_0.png)

**Figure 45.13**

The configurations available with the IIS Manager are grouped with the categories ASP.NET, IIS, and Management settings (see Figure 45.14). Here you can configure Application Settings, Connection Strings, Session State, and more. Mainly, this configuration offers a graphical UI to the XML configuration file `web.config`.

![](img/3d365b72b289213a91ade7eb366b8f35_1761_0.png)

**Figure 45.14**

## Web Deploying to IIS

When you have an application prepared in the IIS Manager, you can directly deploy the web application from within Visual Studio to IIS. Before doing this, create a new empty database named `ProCSharpWebDeploy1` on the server `(localdb)\MSSQLLocalDB`. You can do this from within Visual Studio in the SQL Server Object Explorer. Select SQL Server, Databases, and Add New Database.

With the configuration file `Web.Staging.config`, add the connection string to the new SQL Server database instance and add the transformation as shown to change the connection string defined by `Web.config` (code file `WebDotnetFramework/Web.Staging.config`):

```xml
<connectionStrings>
  <add name="DefaultConnection"
       connectionString="Data Source=(localdb)\MSSQLLocalDB;
       Initial Catalog=WebDeploy1;Integrated Security=True;
       Connect Timeout=30;Encrypt=False;
       TrustServerCertificate=False;ApplicationIntent=ReadWrite;
       MultiSubnetFailover=False"
       providerName="System.Data.SqlClient"
       xdt:Transform="SetAttributes" xdt:Locator="Match(name)" />
</connectionStrings>
```

For deploying the database directly with the deployment, you can configure the Package/Publish SQL configuration with the Project Properties (see Figure 45.15). Here you can import the connection string from the `web.config` file. You can also add custom SQL scripts with the deployment and either deploy only the database schema or also copy the data as well.

![](img/3d365b72b289213a91ade7eb366b8f35_1764_0.png)

**Figure 45.17**

With the Settings tab (see **Figure 45.18**) you configure file publish options. Here, you can select the configuration to choose the corresponding web configuration file. You can precompile the source files during publishing. This way you don’t need to deliver the C# source files with the package. Also, you can exclude files from the `App_Data` folder. This folder can be used for file uploading and a local database. In case you have only test data in this folder, you can safely exclude this folder from the package. Also, you can select the database connection string with the Package/Publish SQL configuration.

**Figure 45.18**

```text
Publish Web
PublishToIIS
Configuration: Staging
File Publish Options
- Remove additional files at destination
- Precompile during publishing Configure
- Exclude files from the App_Data folder
Databases
DefaultConnection
Data Source=(localdb)\MSSQLLocalDB;Initial Catalog=ProCSharpWebDeploy
Use this connection string at runtime (update destination web.config)
Update database Configure database updates
< Prev Next > Publish Close
```

images is that they are huge, containing the complete operating system and every tool needed. Of course, you can use virtual machine images with Microsoft Azure. Prepare an image, and install the web application after installing the web server infrastructure.

This is very different from Docker. Docker is built up using an onion-like system. A layer is built up above another layer. Every layer just contains the differences from the other layer. You can use one already-prepared system that includes the requirements from the operating system, add another layer for the web server, and then add one or more layers for the website you want to deploy. These images are small as only changes are recorded.

If you add the Visual Studio Extension Tools for Docker, you can see another option with the Publish menu: to deploy a Docker image. This deployment is available for Windows Server 2016 as well as different Linux variants. Just select the image you like and deploy your website. Of course, when you’re running on Linux, only .NET Core is available.

## Summary

How you deploy web applications has undergone big changes in the last years. Creating installer packages is rarely used nowadays. Instead, you can directly publish from Visual Studio.

You’ve seen how to publish an Internet Information Server that can be hosted on premise (a custom-managed IIS), as well as how to publish to a server on Microsoft Azure. Using Microsoft Azure, a lot of work managing the infrastructure can be avoided.

You’ve also read about an introduction to Docker, another deployment option that allows creating small prepared images where everything needed for the one running the application is prepared to run.

![](img/3d365b72b289213a91ade7eb366b8f35_1769_0.png)

## Connect with Wrox

- **Participate:** Take an active role online by participating in our P2P forums at p2p.wrox.com
- **Wrox Blox:** Download short informational pieces and code to help you get up to date and out of trouble.
- **Join the Community:** Sign up for our free monthly newsletter at newsletter.wrox.com
- **Wrox.com:** Browse the vast selection of Wrox titles, e-books and blogs and find exactly what you need
- **User Group Program:** Become a member and take advantage of all the benefits
- **Wrox on Twitter:** Follow @wrox on Twitter and be in the know on the latest news in the world of Wrox.
- **Wrox on Facebook:** Join the Wrox Facebook page at facebook.com/wroxpress and get updates on new books and publications as well as upcoming programmer conferences and user group events

## Wiley End User License Agreement

Go to [www.wiley.com/go/eula](www.wiley.com/go/eula) to access Wiley’s ebook EULA.

## Inhaltsverzeichnis

- **Introduction**
  - The Significance of .NET Core
  - The Significance of C#
  - What’s New in C# 6
  - What’s New with the Universal Windows Platform
  - What You Need to Write and Run C# Code
  - What This Book Covers
  - Conventions
  - Source Code
  - Errata
  - p2p.wrox.com
- **Part I: The C# Language**
  - **Chapter 1: .NET Application Architectures**
    - Choosing Your Technologies
    - Reviewing .NET History
    - .NET 2015
    - Hello, World
    - Compiling with .NET 4.6
    - Compiling with .NET Core CLI
    - Application Types and Technologies
    - Developer Tools
    - Summary
  - **Chapter 2: Core C#**
    - Fundamentals of C#
    - Creating Hello, World! with Visual Studio
    - Working with Variables
    - Using Predefined Data Types
    - Controlling Program Flow
    - Working with Enumerations
    - Getting Organized with Namespaces
    - Understanding the Main Method
    - Using Comments
    - Understanding C# Preprocessor Directives
    - C# Programming Guidelines
    - Summary
  - **Chapter 3: Objects and Types**
    - Creating and Using Classes
    - Classes and Structs
    - Classes
    - Anonymous Types
