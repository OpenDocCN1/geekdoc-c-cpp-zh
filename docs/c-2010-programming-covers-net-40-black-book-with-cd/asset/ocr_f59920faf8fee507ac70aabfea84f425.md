# Chapter 36: Security in .NET 4.0

Security message box appears warning you about the effects of the change in permissions. Click the Yes button on the message box and then click the OK button in the Permissions for MyLogo application. Close the MyLogo Properties dialog box by clicking the OK button.

> **NOTE**
> 
> You need to be logged in as an Administrator or a user with similar privileges to have the rights to set permissions for other users. If you set the permissions for the user group to which the intended user belongs, then the permissions apply to all the users that exist in that group.

Now, if a person logs in to the computer with the TestUser account and tries to use the MyLogo application, he is unable to do so. Let’s understand how it happens.

+   10. Log in as the TestUser user and create a Windows Forms application named Invoice (on the CD-ROM). This application attempts to use the MyLogo application but fails to do so. To create the Invoice application, add one button, one group box, one panel, and 10 labels, as shown in Figure 36.17:

![](bbox=[0.205, 0.291, 0.809, 0.615])

To use the WPF user control in the Invoice application, which is a Windows Forms application, you need to add references to the following assemblies:

+   - PresentationCore
+   - PresentationFramework
+   - WindowsBase
+   - WindowsFormsIntegration
+   - MyLogo

You can add references to the PresentationCore, PresentationFramework, WindowsBase, and WindowsFormsIntegration by right-clicking the Invoice project in the Solution Explorer and selecting Add Reference option, which displays the Add Reference dialog box. Select these four assemblies from the .NET tab in the Add Reference dialog box. Let’s now try to add a reference to the MyLogo assembly in the Invoice application.

+   11. Click the Browse tab and go to the location of the MyLogo.dll in the Add Reference dialog box. When you click the OK button in the Add Reference dialog box, an error occurs, as shown in Figure 36.18: