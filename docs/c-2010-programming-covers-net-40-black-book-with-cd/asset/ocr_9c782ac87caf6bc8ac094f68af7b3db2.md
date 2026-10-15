# In Depth

Deployment is a process of distributing the applications for installation on the target computer. This is achieved by creating a setup package and distributing the same using the deployment technologies such as One-Click or Windows Installer. This setup package contains the design, functionality, and the prerequisites required to run the application in an executable format on the target computer.

In this chapter, you learn about different deployment technologies to deploy Windows based and Web-based applications in Visual Studio 2010. The chapter starts with exploring the Windows Installer and ClickOnce deployment technologies for the deployment of applications. Next, you learn different editors and prerequisites required to run an application on the target computer. You also learn to deploy Web-based applications using XCopy deployment and other technologies, such as Web deployment packages and One-Click publishing. In the Immediate section, you learn how to deploy the Windows-based and Web-based applications using different deployment technologies of Visual Studio 2010.

Let’s start with the deployment technologies available in Visual Studio 2010.

# Deployment Technologies in Visual Studio 2010

Visual Studio 2010 provides two technologies, namely, Windows Installer and ClickOnce to deploy the Windows-based applications. The Windows Installer technology creates an installer file (.msi) that distributes the application for deployment. On the other hand, the ClickOnce deployment technology is used to publish an application on a central location and the user installs or runs the application from that location. Let’s learn about these technologies in the following sections.

# Windows Installer Deployment Technology

Windows Installer, also popular as Microsoft Windows Installer (MSI), is a software installation and configuration service that is used to install, maintain, or remove a software application on Windows operating systems. This service contains the information of every application that it installs. The Windows Installer service verifies an application at three levels – product, feature, and component. The product level contains the complete application as a product that a user can install; the feature level contains one or more functionalities of the product; and the component level contains one or more files that are logically related in the application. Note that the files at the component level can be .exe, .dll, or text files.

Windows Installer allows you to deploy Windows and Web applications by creating a Windows Installer Package. The installer package has an extension of .msi and contains the application, any dependent files, registry entries, and others. This installer package can be distributed to various end-users by simply copying it on the target computers. The end-users can then run the installer package to install the application on their computers. When the application is installed, end-users can run the application from the programs list in their computer.

Let’s learn the following in the context of the Windows Installer deployment technology:

+   - Distributable media
+   - Web setup projects
+   - Cab file projects

# Distributable Media

Visual Studio 2010 uses a variety of deployment tools to create Windows Installer (.msi) files. These installer files are distributed to other computers where you want to install the Windows applications. The distribution of these installer files is done through traditional media, such as floppy disks, CD ROM, or DVD. In addition, you can distribute these files on network drive to install across a network.

When you need to deploy an application, at first you are required to add a setup project and specify the settings for deployment properties. It determines the location where you want to save the application and the way the installer would be built. After the Setup project is completely built, two files, ApplicationName.msi and