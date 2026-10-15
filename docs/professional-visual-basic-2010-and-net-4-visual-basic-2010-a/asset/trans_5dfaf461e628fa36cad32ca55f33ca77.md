

<Button Content="Menu Item 6" Width="100" Height="30" Margin="5" />
<Button Content="Menu Item 7" Width="100" Height="30" Margin="5" />
<Button Content="Menu Item 8" Width="100" Height="30" Margin="5" />
<Button Content="Menu Item 9" Width="100" Height="30" Margin="5" />
<Button Content="Menu Item 10" Width="100" Height="30" Margin="5" />
</StackPanel>
</ScrollViewer>
</UserControl>

Code snippet from SilverlightControl1.xaml

As you can see from this example, the StackPanel would grow outside of your design surface, but instead it creates the necessary scrollbars for your content. This gives you the flexibility to put controls inside an area that might be smaller than the area required to display them.

## Border

Last but not least is the Border control, which simply adds a border to a control. Like the ScrollViewer, the Border control only allows one child control. One common use of the Border control would be to add rounded corners using the curved CornerRadius property, as shown in this example:

```
<UserControl x:Class="SilverlightApplication1.SilverlightControl1"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
d:DesignHeight="300" d:DesignWidth="400">

<Grid x:Name="LayoutRoot" Background="White" >
<Border BorderBrush="Silver" BorderThickness="1" Height="263"
HorizontalAlignment="Left" Margin="12,25,0,0"
Name="Border1" VerticalAlignment="Top" Width="376"
Background="Gray" CornerRadius="20">
<Grid Name="Grid1">
<Button Content="Button" Height="23" Name="Center"
VerticalAlignment="Center" Width="75" />
</Grid>
</Border>
</Grid>
</UserControl>
```

Code snippet from SilverlightControl1.xaml

Although the Border control is simple, it does help add a small improvement to the overall look and feel of your content.

## ADDING ITEMS TO THE SILVERLIGHT PROJECT

As with all other .NET projects, you will need to add more than just the basic items provided when you first create a Silverlight project, and Silverlight offers several different options. Most are very similar to what you will find in other project types in Visual Studio, but many are unique to Silverlight.

You will find all of these options when you right-click on your Silverlight project and select Add New Item, as shown in Figure 19-8.

![](img/d99870e80390742f93963da7be0b2e61_702_0.png)

## FIGURE 19-8

The following sections provide a brief overview of each item type and when to use it.

## Silverlight User Control

The Silverlight User Control is probably the most common item you will add to your Silverlight project. It is almost exactly like adding a user control in a Windows Forms application or a WPF project. Selecting it will provide you with both a XAML and .vb code-behind file. This is where you can create the user interface for your controls.

## Silverlight Application Class

The Silverlight Application Class is similar to what you have learned earlier in the chapter about the App.xaml because this is exactly what the App.xaml is. The only time you would probably create a Silverlight Application Class is when you have created a Silverlight project and removed your App.xaml, or you created a Silverlight Class Library and wanted to convert it to a complete application.

## Silverlight Page

The Silverlight Page is very similar to a page in ASP.NET and is what works with the navigation framework described earlier in the chapter. The only real difference is the capability to set the Page title that will show in the browser title bar. For a basic page the code looks like this:

```
<navigation:Page x:Class="SilverlightApplication1.Page1"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
xmlns:navigation="clr-namespace:System.Windows.Controls;
assembly=System.Windows.Controls.Navigation"
d:DesignWidth="640" d:DesignHeight="480"
Title="Page1 Page" >
```

```
<Grid x:Name="LayoutRoot">
</Grid>
</navigation:Page>
```

## Silverlight Child Window

The Silverlight Child Window is a modal dialog within Silverlight that gives you the look and feel of a Windows Forms modal dialog. When you create a Child Window you will get a design surface that looks like the one shown in Figure 19-9.

To show this Child Window you would use the following code:

```
Dim nWnd as New ChildWindow1
nWnd.Show()
```

When a Child Window is shown, you will see a nice animation of the window zooming in; and when it is hidden, it will zoom out. This adds a nice touch to your application.

![](img/d99870e80390742f93963da7be0b2e61_703_0.png)

## Silverlight Template Control

A Silverlight Template Control is a class that has an existing control as its base class. It is similar to a control template in Windows Forms or WPF. Unlike a User Control, it does not have a design surface, but when compiled it does create a class which is available in the Toolbox window for use as a control.

## Silverlight Resource Dictionary

Last but not least is the Silverlight Resource Dictionary. This class enables you to centralize things like templates, styles, and more. It also creates a simple way to organize these items into separate files for better manageability.

## SILVERLIGHT OUT OF THE BROWSER

One of the features introduced in Silverlight 3 is “out of the browser” capabilities. This feature allows your users to create a desktop and start menu icon for your application. It also enables your application to run out of the browser even when there is no Internet connection. These features are not just limited to the PC, but also work on the Mac, so now you can build cross-platform .NET applications without having to use something like the Mono Project to develop them.

To enable Out of the Browser options, simply right-click on your Silverlight project and click Properties. Then you can simply check “Enable running application out of the browser.” That’s it — you have just made your Silverlight application capable of running out of the browser on both a PC and a Mac. To set up a few more options, you can click the Out-of-Browser Settings button, which will bring up the dialog shown in Figure 19-10.

![](img/d99870e80390742f93963da7be0b2e61_703_1.png)

From here you can set several additional options, including the title of the window, window size, and icon options. When you define these settings under the Properties window, you are actually creating an `OutOfBrowserSettings.xml` file under the My Project folder, which can be viewed by clicking the Show Hidden Files button on the Solution Explorer. Here is a sample `OutOfBrowserSettings.xml` file:

```
```xml
<OutOfBrowserSettings>
  ShortName="SilverlightApplication1 Application"
  EnableGPUAcceleration="False"
  ShowInstallMenuItem="True">
    <OutOfBrowserSettings.Blurb>SilverlightApplication1 Application on your desktop;
        at home, at work or on the go.
    </OutOfBrowserSettings.Blurb>
    <OutOfBrowserSettings.WindowSettings>
      <WindowSettings Title="SilverlightApplication1 Application" />
    </OutOfBrowserSettings.WindowSettings>
    <OutOfBrowserSettings.Icons>
      <Icon Size="16,16">MyIcon.png</Icon>
      <Icon Size="32,32">MyIcon.png</Icon>
      <Icon Size="48,48">MyIcon.png</Icon>
      <Icon Size="128,128">MyIcon.png</Icon>
    </OutOfBrowserSettings.Icons>
</OutOfBrowserSettings>
```
```

Of course, this just describes the setup for running your application out of the browser. To actually install the application, there are two options for installing the application: by right-clicking the application and selecting install or by initiating it from the code.

Let’s take a look at the first option. After setting your application to run out of the browser, actually run your application. You will see that it runs just as you expect. Now right-click the application. You will be presented with the dialog shown in Figure 19-11.

Once you have installed the application, it will run the Silverlight application in what seems to be a standalone application. This application will automatically update itself to the version hosted on in your Asp.NET application. To uninstall the running application, right-click on it.

![](img/d99870e80390742f93963da7be0b2e61_704_0.png)

The second way of installing the application, from code, is actually very simple — only one line of code:

```
```text
App.Current.Install()
```
```

That’s it! You can create a button and call the Install function to install the application locally.

## SUMMARY

This chapter has only briefly described a diverse set of features from Silverlight, as entire books could be written about Silverlight and its various elements. In this chapter you have learned how to do basic layout and design, and have seen how it relates to other technologies that you have learned in previous chapters. We will continue with Silverlight in the next chapter to dig deeper into building more complex applications, and how to interact with Web services, including SOAP and WCF to interact with data. We will also build on your knowledge of Visual Basic and Silverlight to create a Model View View-Model application which enables better separation of concerns for your application.

