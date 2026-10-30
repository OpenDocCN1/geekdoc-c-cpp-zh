The Signing, Security, and Publish Tabs The settings on the Signing, Security, and Publish tabs are used for ClickOnce deployment. Using ClickOnce deployment, you can set up applications to be deployed and updated on multiple sites via the Web. This technique is primarily used by large organizations to facilitate deploying applications to many users.

# Deploying Windows Applications

Most of this text is devoted to writing and testing applications using the Visual Studio IDE. However, once you get an application tested and ready for use, you will want to deploy it and run it on another computer. To run a .NET Windows application, the target computer must have the .NET Framework or the .NET Framework Redistributable installed. The Redistributable file is available for free download on Microsoft's Web site and is available for Windows XP and Vista.

You can choose from several methods for deploying your Windows applications: (1) XCopy deployment, (2) Windows Installer technology, (3) ClickOnce deployment, or (4) third-party installer products.

XCopy deployment gets its name from the old DOS XCOPY command, which copied all files in the current folder and all subfolders. Although you can use the XCOPY command for copying files, XCopy deployment simply means that you copy the necessary files from the development machine to the target machine.

Deploying a compiled Windows application can be as easy as copying the .exe file from the bin folder to another computer. This technique is not very robust but can work for a simple installation. However, deploying a Web application is a little more complicated because more than one file is needed to run an application.

Microsoft Windows Installer is a separate application that ships with Windows. The installer creates .msi files that contain the application and any support files needed for deployment. Deployment is covered in Appendix C.

# The VB My Objects

The Visual Basic My object provides several objects and properties. My gives you easy access to information about your application and its resources, the computer on which the application is executing, and the current user.

It is easy to discover the available objects using IntelliSense (Figure 1.9): Application, Computer, Forms, Resources, Settings, User, and Web Services.

![](bbox=[0.28, 0.84, 0.5, 0.98])

# Figure 1.9

Type "My." to see the available My objects in IntelliSense.