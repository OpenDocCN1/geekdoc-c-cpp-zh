# Using Role-Based Security to Authenticate and Authorize Users

Nowadays, most modern operating systems come with their own security system that allows you to authenticate users. In many situations, the security system of the underlying operating system meets the security requirements of your .NET applications adequately. However, there may be some situations where this security system may not provide the desired level of security to your applications. In such cases, you can employ role-based security to give an extra edge of security to your applications. With role-based security, you can secure not only an entire application but also the individual classes and methods in the application.

Let's first get a grasp on how the security infrastructure of the Windows operating system works and then understand where the role-based security comes in the picture. For this, you need to create two applications – one that needs to be secured and the other that requests the secured application. You need to create the secured application using administrator account and set the permissions such that it is not accessible under a particular Windows user account (say TestUser). Then, you need to create the requesting application under the denied user account (on the same computer) and try to access the secured application. You will notice how the requesting application is unable to access the secured application.

Let's now create a WPF User Control Library application named MyLogo (available on the CD-ROM) under an administrator user account on Windows Vista. The MyLogo application is the application that needs to be secured. To create the MyLogo application, perform the following steps:

+   1. Select File→New→Project to open the New Project dialog box in the Visual Studio 2010 IDE. In the dialog box, select the Visual C#→Windows option in the Project types and the WPF User Control Library option in the Templates pane. Specify MyLogo as the name of the application, select an appropriate location, and click the OK button. The MyLogo application is created.
+   2. Open the UserControl1.xaml file in the MyLogo application and add the code given in Listing 36.3:
+   3. Compile the application. After you compile the MyLogo application, you need to set the permissions for one or more users. Note that the Windows operating system uses the access control lists (ACLs) to set the permissions on all the files, folders, and other resources. An ACL is a list of users and the permissions that the users have for a particular resource.
+   4. Navigate to the location of the MyLogo assembly on the computer, which is in the MyLogo\bin\Debug folder of the application.
+   5. Right-click the MyLogo.dll assembly and select the Properties option from the context menu. The MyLogo Properties dialog box appears, as shown in Figure 36.13:

# Listing 36.3: Creating the MyLogo Application

```
<UserControl x:Class="MyLogo.UserControl1"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Height="30" Width="30" Background="LawnGreen" BorderBrush="RoyalBlue" BorderThickness="5">

<Grid>
<Ellipse Name="ellipse1" Height="10" Width="25" Stroke="Red" StrokeThickness="5"/>
<Ellipse Name="ellipse2" Height="25" Width="10" Stroke="Yellow" StrokeThickness="5"/>
</Grid>

</UserControl>
```

> NOTE
> The ACL feature is available only on New Technology File System (NTFS).

To control the access of the MyLogo application to other users on the computer, you need to set permissions on the MyLogo assembly (MyLogo.dll).