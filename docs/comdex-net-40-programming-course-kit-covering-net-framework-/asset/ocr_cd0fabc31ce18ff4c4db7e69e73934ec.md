Deploying an application refers to the process of distributing the application among various end-users. You might wonder why to share an application with others. Let’s consider an example to understand the need of deploying applications. Suppose you have developed a currency converter application that converts the values of one currency into another. You can use the application only for your company’s benefit. However, if you choose to share the application with other companies, it will prove to be useful to them as well. In addition, other companies may contribute towards further improvement of the original application. You need to deploy the currency converter application to enable other companies to use and modify it. Traditionally, applications are deployed using scripted set-up programs. These set-up programs were based on the procedural model and focused on how to deploy an application. The deployment in Visual Studio is much easier and flexible as compared to the traditional approach of deploying applications because it provides different deployment techniques, such as Windows Installer and XCopy.

In this appendix, you learn about the enhancements in deployment techniques. Next, you learn about the Web deployment features available in Visual Studio 2010. Further, you learn about deploying a Windows application and an ASP.NET website. Finally, you learn how to deploy a Web application by using one-click publish.

Let’s start by discussing new features or enhancements in deployment techniques.

# Exploring Enhancements in Deployment Techniques

Prior looking at the different steps involved in setting up and deploying Web applications, it is important to know about the different enhancements in Visual Studio 2010 deployment techniques. Visual Studio provides many deployment techniques, namely Windows Installer, XCopy, Publish, Web One Click Publish, and Copy Web Site, to deploy Web applications. Based on factors, such as type of application, type of end-users, and frequency of updates, you can use different deployment techniques to deploy your application. Now, let’s look at the deployment techniques in the following sections.

# Windows Installer Deployment

Windows Installer is a software installation and configuration service that ships with the Windows operating system. The Windows Installer service contains the record of information about every application that it installs. However, before installing the application, Windows Installer divides it into three levels, which are as follows:

+   - **Product**—Refers to a complete application that a user can install
+   - **Feature**—Refers to any functionality of a product
+   - **Component**—Refers to a single file or multiple files that are logically related. These files can be .exe, .dll, or a simple text file.

![](bbox=[0.205, 0.63, 0.271, 0.675])

> > You can use Windows Installer to deploy both Windows and Web applications.

Windows Installer deploys applications with the interactive setup wizard. It provides professional deployment and a standard format for component management. This technique has been greatly enhanced for Windows 7 and the applications developed under .NET Framework. Now, let’s see what the Windows Installer deployment technique offers for Windows 7.

# Windows 7 Support

The Windows Installer deployment technique has been updated up to an extent that a user can smoothly install an application on Windows 7, even when the User Account Control (UAC) setting is enabled. Typically, the installations do not prompt for further steps when setup starts; however, the application and the components are elevated if necessary. When the installation starts, the requested elevation is displayed in a message box with additional instructions. The following are the different types of requested elevations: