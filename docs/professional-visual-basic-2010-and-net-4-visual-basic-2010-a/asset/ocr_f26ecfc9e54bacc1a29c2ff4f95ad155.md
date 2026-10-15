> In order to run the development environment for Windows Azure, you need to run Visual Studio 2010 as an administrator. Otherwise, you will see the error message shown in Figure E-10 when you attempt to run your application. To run Visual Studio as an administrator in Windows Vista or Windows 7, right-click the icon and select Run as Administrator. You may be required to enter your user ID and password at this point.

In addition, in order to deploy your applications to the cloud, you need to obtain a developer key. This key is also used for all requests for data. Currently, you get a key by making a request at http://go.microsoft.com/fwlink/?LinkID=129453. However, developing using the Windows Azure Tools for Visual Studio does not require this key, only when you are deploying your application to the live servers.

You need to exit Visual Studio to install the tools. After you run the installer, you will see the option enabling you to create an Azure service (see Figure E-11).

![](bbox=[0.5, 0.21, 0.88, 0.35])

FIGURE E-10

![](bbox=[0.09, 0.41, 0.67, 0.73])

FIGURE E-11

# Creating a Windows Azure Project

To explore the features available when creating applications with Windows Azure, create a new project called CloudToDo.

Selecting that option brings you to the New Cloud Service Project dialog (see Figure E-12). This dialog enables you to select the initial types of service you will be creating. Of course, you can add others to your project later.

![](bbox=[0.52, 0.76, 0.88, 0.94])

FIGURE E-12