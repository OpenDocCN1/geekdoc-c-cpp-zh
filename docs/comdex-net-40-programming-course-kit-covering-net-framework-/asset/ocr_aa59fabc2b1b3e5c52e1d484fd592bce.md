| Table 11.1: Controls in Silverlight 4.0 |  |  |
|---|---|---|
| **Control** | **Description** | **XAML Element Example** |
| TextBox | Allows you to display text or obtain input from a user. In Silverlight 4.0, the TextBox control can display text in multiple lines and wrap the text according to its size. | `<TextBox Text="Hello, this is the TextBox control in Silverlight 4.0." IsReadOnly="False" Height="75" Width="75" TextWrapping="Wrap" />` |
| TreeView | Displays data items in a hierarchical manner. | `<sdk:TreeView>\n<sdk:TreeViewItem Header="Object-Oriented Programming Languages" FontFamily="Georgia" FontSize="12" Foreground="HotPink" />\n<sdk:TreeViewItem Header="Java" FontFamily="Courier New" FontSize="10" Foreground="MidnightBlue"></sdk:TreeView>\n` |
| ViewBox | Resizes itself according to the size of its content and the space available to it. | `<ViewBox MaxWidth="300" MaxHeight="300">\n<Image Source="Flowers.jpg" />\n</ViewBox>` |
| WebBrowser | Enables you to navigate to specified Uniform Resource Identifiers (URIs) and create your own custom Silverlight browsers. | `<WebBrowser x:Name="browserControl" Grid.ColumnSpan="2" Width="428" />` |

Now, let’s learn to develop Silverlight applications using Visual Studio 2010.

# Developing Silverlight Applications

Silverlight provides you the functionality to develop Web sites that can host multimedia and animations. You already know that Visual Studio 2010 is the best choice to create a Silverlight application as in Visual Studio 2010; you can create a Silverlight application using any .NET Framework language. Visual Studio 2010 allows you to integrate other Web applications, such as the ASP.NET AJAX Web application, with a Silverlight application.

In this section, you learn to perform the following tasks:

+   - ☐ Creating a Silverlight application
+   - ☐ Hosting video in a Web site
+   - ☐ Creating applications using different controls

Let’s perform these tasks one by one.

# Creating a Simple Silverlight Application

Now, you learn to create a Silverlight application. In this application, the GridSplitter control is used so that a user can resize rows and columns of the grid. To create a Web site MyFirstSilverlightApp (also available on the CD), perform the following steps:

+   1. Open Microsoft Visual Studio 2010 from the start menu.
+   2. Select File→New→Project, as shown in Fig. ASP-11.14: