
Setup.exe can be found in its Debug folder. You need to copy the .msi file from the build location to distributable media, such as floppy disk and CD, to deploy the application. Similarly, to deploy the application to a network location, you need to copy the .msi file to the server computer, from where it can be downloaded by network users.

## Web Setup Projects

In traditional media distributing system, you deploy an application by copying its executable file to a media device (for instance CD) and then to a Web server. However, Visual Studio 2010 supports deployment of an application to a Web server directly as it includes the deployment tools for this purpose. Deploying a Web application directly to a Web server has its own advantages as it automatically handles the issues raised with registration and configuration. In addition, a Web application is deployed to a Web server; the user can directly download and run it from a Web server.

You can deploy a Web application to a Web server by first creating and building a Web Setup project and copying it to the Web server. Then, you need to run the installer to install the application on the Web server using the specified settings of the Web Setup project. The key difference between the Setup and Web Setup projects is that the Web Setup project deploys the application to a virtual directory on the Web server, whereas the setup project deploys the application to a folder on the target computer.

## Cab File Projects

Cab file projects are used to create cabinet files (.cab) that can download components to a Web browser, such as ActiveX controls. The Cab file projects add the files and project outputs via Solution Explorer and set the properties in the Properties windows or Project Property pages.

The properties of the Cab file allow you to specify a compression level; implement authentication; set the display name and version information; and specify the location of dependant files on the Web. The Cab file projects are used when you want to run the code on a client computer instead of a server.

## ClickOnce Deployment Technology

ClickOnce is a deployment technology that allows you to publish Windows-based applications on a Web server or network file share location. Visual Studio 2010 provides the full support for the ClickOnce deployment technology to publish and update the applications. The ClickOnce deployment technology allows you to deploy the self-updating Windows-based applications. It also supports the deployment of WPF XAML Browser Applications (XBAPs). XBAP is a Windows technology used to create rich Internet applications just similar to WPF applications. Note that WPF is a Windows application that does not support Web browsers; whereas an XBAP application can be easily hosted on a Web browser.

In Visual Studio 2010, the ClickOnce deployment technology is enhanced with the following features:

- **Support for .NET Framework 4.0 version** — Creates applications by using Visual Studio 2010 that can target .NET Framework 4.0 and its new features.
- **Support for multiple versions of the .NET Framework** — Creates applications that are compatible with multiple versions of the .NET Framework. Take for instance; you can specify the target framework for an application as .NET Framework 3.5 or .NET Framework 4.
- **Enhanced logging feature** — Stores logging information that includes various parameters passed to the ClickOnce runtime, the browser settings, and ClickOnce security options.
- **Custom Installer and User Interface** — Allows you to create a custom graphical user interface for installing and updating the .exe applications. In addition, the custom installer can have custom dialog boxes for security and maintenance operations.

To deploy a Windows-based application using the ClickOnce deployment technology, you need to publish the application by making the application available to end-users. To publish an application, you need to use the Publish Wizard or the Publish page in the project properties dialog box to set the publish properties of the application. The Publish Wizard allows you to specify the location where you want to publish the application, such as Web server, network or file share, or removable media.

The ClickOnce deployment technology allows you to deploy applications by selecting one of the following options:

- **To install from the Web or a network share**—Deploys an application either on the Web or a shared network. You should apply this setting for applications that cater to users of high-speed Internet connection or Local Area Network (LAN). To install the application, the end-user only has to click the icon on the Web page or double-click an icon on the file share. Applications that are deployed using this setting are automatically added to the Start menu and the Add/Remove Programs menu.

- **To install from a CD or DVD**—Deploys an application on a removable disk, such as, CD or DVD. This setting is best suited for applications that would be used by users who have irregular or low-bandwidth network connections. Note that in this case, you do not need any network connection to execute the application but you do need a connection for updating the application.

- **To start from the Web or a network share**—Deploys a Windows application as a Web application. It is suitable for those applications that are not used very often and hence does not require to be permanently installed on the end-user’s computer. In this case, when you click on the application’s icon on the Web page or on the file share, the application starts executing. Since the application is not installed on the end-user’s computer, you cannot view it either on the Start menu or on the Add/Remove Programs menu.

Next, let’s learn about the ClickOnce application cache.

## Application Cache

When a ClickOnce application is installed locally or hosted online, it is stored in the ClickOnce application cache of the client computer. The ClickOnce application cache is a set of hidden directories placed under the Local Settings directory of the current user’s Documents and Settings folder. The application cache contains all the application files, assemblies, configuration files, application and user settings, and data directory. If the application is created in earlier versions, the application cache is responsible to migrate the data directory of the application to the latest version. In case the ClickOnce applications are hosted online, the size of the ClickOnce application cache gets limited to a specified amount; whereas the installed applications do not restrict to the cache size limitation. The cache storage quota is responsible to determine the size of the application cache.

Let’s now learn about security in the ClickOnce deployment.

## Security

The security is a major concern when you are going to distribute an application among various users. The ClickOnce deployment deploys the applications with a limited set of permissions, which are based on the location from which the original version of the application was deployed by default. However, when the application is updated, the permission is also updated accordingly.

The ClickOnce deployment technology is a trustworthy deployment technology for smart client applications. This means that the deployed applications do not harm the client’s computer by any means. The ClickOnce security enables protection for the client computer at the time of installation and runtime. The usage of ClickOnce can ensure the user about the safety of the application.

In addition, ClickOnce applications are protected at runtime that is based on application’s identity. This enables the low-privilege users to deploy the applications without administrator interference. However, this does not mean that your application is unprotected from the user perspective. Using the .NET role-based security, you can prevent users from using functionalities in your application if they are not allowed to use them.

ClickOnce security is provided as soon as the application is deployed on the client computer. All the files are placed separately in different directories under the application cache. Alternatively, to provide the runtime protections for the applications, ClickOnce relies on the Code Access Security (CAS) infrastructure of the .NET Framework. The CAS provides a security mechanism by using Windows access control and .NET role-based security.

Next, you learn about different editors that are available for creating an installer file.
