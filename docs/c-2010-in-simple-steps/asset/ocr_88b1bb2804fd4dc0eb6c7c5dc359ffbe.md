After the installation is complete, the Installation Complete page appears.

+   40. Click the Close button to successfully complete the FillColorSetup wizard.
+   41. Run the newly installed FillColor application from the location where you have installed it or by selecting Start→All Programs→FillColor. The output appears, as shown in Fig.C#-14.17:

![](bbox=[0.32, 0.24, 0.6, 0.44])

Fig.C#-14.17

This completes creating and deploying an application by using Windows Installer. Let's learn to deploy an application by using ClickOnce.

# Deploying Applications Using ClickOnce

ClickOnce deployment is used to deploy Windows application on the Web server or network file share. It provides a simplified installation experience to the end user. Using the ClickOnce deployment, you can enable the self-update feature of Windows applications that can be installed, updated, and run from a website with minimal user interaction. The self-updating feature enables you to download only the updated portions of the application. The ClickOnce deployment method deploys an application by using the Publish Wizard. The Publish Wizard enables you to publish an application to a Web page, a network file share, or a CD. In other words, ClickOnce is an easy technique to install Web applications as compared to the Windows installer deployment technique. Using ClickOnce you can install Windows applications through a simple click. Let's perform the following steps to deploy an application using ClickOnce (in this case, we deploy the FillColor application, which we have created in the previous section):

+   1. Click Start→All Programs→Microsoft Visual Studio 2010→Microsoft Visual Studio 2010.
+   2. Right-click Microsoft Visual Studio 2010 and select Run as administrator option from the context menu that appears.
+   3. Create a Windows Forms Application named FillColour.
+   4. Repeat steps 6 to 14 of Deploying Applications by Using Windows Installer section of this chapter.
+   5. Right-click the FillColour project node in Solution Explorer and then select the Publish option from the context menu, as shown in Fig.C#-14.18: