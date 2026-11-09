
![](img/9862a98a1a2d3bb14334137965a1ec60_731_0.png)

Fig. ASP-11.38

With this, we come to the end of the chapter. Now, let’s summarize the main points of the chapter.

## Summary

In this chapter, you have learned about the Silverlight technology. Further, you have learned about its main features along with the new features introduced in Silverlight 4.0. Moreover, this chapter discussed the architecture of Silverlight 4.0 and the installation of the Silverlight 4.0 Tools. Finally, you have learned to develop Silverlight applications using the Silverlight controls in Visual Studio 2010.

## Appendix: Deployment

![](img/9862a98a1a2d3bb14334137965a1ec60_732_0.png)

**In this Appendix:**

- Exploring Enhancements in Deployment Techniques
- Web Deployment Features in Visual Studio 2010
- Deploying a Windows Application
- Deploying an ASP.NET Web Site
- Deploying a Web Application using One-Click Publish

Deploying an application refers to the process of distributing the application among various end-users. You might wonder why to share an application with others. Let’s consider an example to understand the need of deploying applications. Suppose you have developed a currency converter application that converts the values of one currency into another. You can use the application only for your company’s benefit. However, if you choose to share the application with other companies, it will prove to be useful to them as well. In addition, other companies may contribute towards further improvement of the original application. You need to deploy the currency converter application to enable other companies to use and modify it. Traditionally, applications are deployed using scripted set-up programs. These set-up programs were based on the procedural model and focused on how to deploy an application. The deployment in Visual Studio is much easier and more flexible as compared to the traditional approach of deploying applications because it provides different deployment techniques, such as Windows Installer and XCopy.

In this appendix, you learn about the enhancements in deployment techniques. Next, you learn about the Web deployment features available in Visual Studio 2010. Further, you learn about deploying a Windows application and an ASP.NET website. Finally, you learn how to deploy a Web application by using one-click publish.

Let’s start by discussing new features or enhancements in deployment techniques.

### Exploring Enhancements in Deployment Techniques

Prior to looking at the different steps involved in setting up and deploying Web applications, it is important to know about the different enhancements in Visual Studio 2010 deployment techniques. Visual Studio provides many deployment techniques, namely Windows Installer, XCopy, Publish, Web One-Click Publish, and Copy Web Site, to deploy Web applications. Based on factors, such as type of application, type of end-users, and frequency of updates, you can use different deployment techniques to deploy your application. Now, let’s look at the deployment techniques in the following sections.

### Windows Installer Deployment

Windows Installer is a software installation and configuration service that ships with the Windows operating system. The Windows Installer service contains the record of information about every application that it installs. However, before installing the application, Windows Installer divides it into three levels, which are as follows:

- **Product**—Refers to a complete application that a user can install
- **Feature**—Refers to any functionality of a product
- **Component**—Refers to a single file or multiple files that are logically related. These files can be .exe, .dll, or a simple text file.

![](img/9862a98a1a2d3bb14334137965a1ec60_733_0.png)

> You can use Windows Installer to deploy both Windows and Web applications.

Windows Installer deploys applications with the interactive setup wizard. It provides professional deployment and a standard format for component management. This technique has been greatly enhanced for Windows 7 and the applications developed under .NET Framework. Now, let’s see what the Windows Installer deployment technique offers for Windows 7.

### Windows 7 Support

The Windows Installer deployment technique has been updated to an extent that a user can smoothly install an application on Windows 7, even when the User Account Control (UAC) setting is enabled. Typically, the installations do not prompt for further steps when setup starts; however, the application and the components are elevated if necessary. When the installation starts, the requested elevation is displayed in a message box with additional instructions. The following are the different types of requested elevations:

- **Application elevation**—Deploys two files, ApplicationName.msi and Setup.exe. The ApplicationName.msi file contains information about the application; whereas, the Setup.exe file, also known as bootstrapper, contains setup files that require current user’s credentials for execution.
- **Administrator-assisted elevation**—Requires administrator’s credentials, such as the administrator’s username and password, to execute an application. To support this feature, bootstrapper sets the `AdminUser` property to True when Windows 7 is running on your computer.
- **Prerequisite elevation**—Supports prerequisite elevation of components if necessary. Bootstrapper itself performs one elevation. When UAC is enabled in Windows 7, an elevation is prompted for each prerequisite component that has to be elevated, until and unless the component is already installed. If the elevation fails, it results in the failure of bootstrapper and an appropriate message is displayed.
- **Custom action elevation**—Refers to an elevation that is created and executed by Windows 7 in the Custom Actions Editor. The custom actions cannot access user-specific data, such as the registry or file system, because they cannot run in the current user’s account.

Let’s now learn about the Web deployment features in Visual Studio 2010.

### Web Deployment Features in Visual Studio 2010

When you have developed, tested, and debugged an application, the next step is to deploy it. The purpose of deploying an application is to ensure a simple and easy installation for application files and any other required files on a client computer. The .NET Framework provides you with some easy ways to deploy a Web application. You can deploy a Web application by copying its content to the destination, by publishing it, or by using Web Installer. Visual Studio 2010 includes some new features to make the deployment easier for the user. These features are as follows:

- Web packaging
- Web.config transformation
- Database deployment
- One-Click Publish for Web Applications

Let’s discuss these features, one by one.

### Web Packaging

In Visual Studio 2010, the MSDeploy tool is included that is used to create compressed files for a Web application. The compressed files are known as Web package. The Web package contains metadata and the additional information, which is as follows:

- Settings of the Internet Information Server (IIS), including application pool settings and error page settings
- Web application content, which includes Web pages, user controls, and static content
- Schemas of the Structured Query Language (SQL) Server database and the data
- Settings of the registry, components to be installed in the Global Assembly Cache, and security certificates

There are two methods of installation of Web package. In the first method, you can copy the application on the server and then install the application manually with the help of the IIS server. In this method, you can use the command-line commands or deployment Application Programming Interface (APIs) for the deployment of the application.

### Web.config Transformation

Visual Studio 2010 includes a new feature for the deployment of Web application which is known as XML Document Transform (XDT). This feature helps you in transforming the web.config file for production settings from the development settings. The transformation settings are given in the transform files called web.debug.config and web.release.config. The transform files include the changes and the actions needed for the deployment of the web.config file. The changes can be specified in the web.config file and the transformation actions can be specified using the attributes of Extensible Markup
