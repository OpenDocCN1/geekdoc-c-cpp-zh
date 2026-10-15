
In the preceding listing, the System.Windows.Data namespace is added to the SilverlightDataPager application. An instance of the PagedCollectionView class, called pagedcollectionview is also created. The string, WELCOMETOSILVERLIGHT3, is passed to the object, pagedcollectionview, and the String.Split() method is also used. The String.Split() method returns a string array and is used to find all the substrings in a string that are separated by one or more characters.

- 3. Run the SilverlightDataPagerCS application. The output appears, as shown in Figure 17.43:

![](img/e073a4882197be4ab61103cbe0bcb394_933_0.png)

## Figure 17.43: Displaying Output of the SilverlightDataPagerCS Application

- 4. Click any of the page numbers in the DataPager visible at the bottom of the page. The output appears, as shown in Figure 17.44:

![](img/e073a4882197be4ab61103cbe0bcb394_933_1.png)

## Figure 17.44: Displaying the Output After Selecting the Fourth Page

As seen in Figure 17.44, the DataPager control, myPager, displays the data items of the fourth page in the DataGrid control. Next, let’s discuss about the TreeView control.

## Using the TreeView Control

As stated earlier, you know that a Silverlight TreeView control can be used to display hierarchical data in the form of nodes. A node that contains child nodes in a TreeView control can be collapsed and expanded as well. You can click on any node of a TreeView control to collapse it or expand the node to reveal its child nodes. The TreeView control is a specialized ItemsControl control, which means that you can populate the TreeView control with some content by either setting its Items or ItemsSource properties. Now, perform the following steps to use the TreeView control in a Silverlight application:

- 1. Create a Silverlight application named SilverlightTreeViewCS (available on the CD). Listing 17.18 shows the code for the MainPage.xaml file of the SilverlightTreeViewCS Silverlight application:

### Listing 17.18: Showing the Code for the MainPage.xaml File of the SilverlightTreeViewCS Application

```
<UserControl xmlns:my="clr-namespace:System.Windows.Controls;assembly=System.Windows.Controls" x:Class="SilverlightTreeViewCS.MainPage" xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" xmlns:d="http://schemas.microsoft.com/expression/blend/2008" xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" mc:Ignorable="d" d:DesignHeight="300" d:DesignWidth="400">
<Grid x:Name="LayoutRoot">
<my:TreeView Background="Beige">
<my:TreeViewItem Header="Programming Languages" Foreground="Red" FontFamily="Comic Sans MS" FontSize="15" FontWeight="Bold">
<my:TreeViewItem Header="Structured Programming Language" FontFamily="Georgia" FontSize="12" Foreground="HotPink">
<my:TreeViewItem Header="C" FontFamily="Courier New" FontSize="10" Foreground="MidnightBlue"/>
</my:TreeViewItem>
<my:TreeViewItem Header="Object-Oriented Programming Languages" FontFamily="Georgia" FontSize="12" Foreground="HotPink">
<my:TreeViewItem Header="Java" FontFamily="Courier New" FontSize="10" Foreground="MidnightBlue"/>
<my:TreeViewItem Header="C#" FontFamily="Courier New" FontSize="10" Foreground="MidnightBlue"/>
<my:TreeViewItem Header="VB.NET" FontFamily="Courier New" FontSize="10" Foreground="MidnightBlue"/>
</my:TreeViewItem>
<my:TreeViewItem Header="Dynamic Languages" FontFamily="Georgia" FontSize="12" Foreground="HotPink">
<my:TreeViewItem Header="Python" FontFamily="Courier New" FontSize="10" Foreground="MidnightBlue"/>
<my:TreeViewItem Header="Ruby" FontFamily="Courier New" FontSize="10" Foreground="MidnightBlue"/>
</my:TreeViewItem>
</my:TreeViewItem>
</my:TreeView>
</Grid>
</UserControl>
```

2. Run the SilverlightTreeViewCS application. The output appears, as shown in Figure 17.45:

![](img/e073a4882197be4ab61103cbe0bcb394_934_0.png)

## Figure 17.45: Displaying Output of the SilverlightTreeViewCS Application

As you can see in Figure 17.45, the root node of the TreeView control is visible.

- 3. Click the triangular glyph on the left side of the root node, Programming Languages, to expand it and view its child nodes. The output after expanding the root node appears, as shown in Figure 17.46:

![](img/e073a4882197be4ab61103cbe0bcb394_935_0.png)

Figure 17.46: Displaying the Output After Expanding the Root Node

As seen in Figure 17.46, the root node of the TreeView control displays its child nodes. You can further expand the child nodes to view their child nodes.

Next, let’s create an application to learn how to integrate Silverlight with ASP.NET applications.

## Integrating Silverlight with ASP.NET Applications

You have already learned in the In Depth section that you can easily integrate Silverlight with ASP.NET applications. Now, perform the following steps to create an application to learn how to integrate Silverlight and an ASP.NET application.

- 1. Create an application named AnimatedButtonAppCS (available on the CD). For this, open the Visual Studio IDE and select File→New→Project. The New Project dialog box appears. Under the Installed Templates pane, select Visual C# →Silverlight and from the middle pane, select Silverlight Application. Specify the name of the application as AnimatedButtonAppCS and enter an appropriate location to save the application.

- 2. Click the OK button, which displays the New Silverlight Application dialog box (Figure 17.47).

- 3. Select the Host the Silverlight application in a new Web site check box and click the OK button, as shown in Figure 17.47:

![](img/e073a4882197be4ab61103cbe0bcb394_935_1.png)

Figure 17.47: Selecting the Option to Host the Silverlight Content in a Web Site

4. Open the MainPage.xaml file of the AnimatedButtonAppCS application and add the code, as shown in Listing 17.19:

### Listing 17.19: Showing the Code for the MainPage.xaml File

```
<UserControl x:Class="AnimatedButtonAppCS.MainPage"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
d:DesignHeight="450" d:DesignWidth="450">

<Grid x:Name="LayoutRoot" Background="Red">
    <Grid.Triggers>
        <EventTrigger RoutedEvent="Grid.Loaded">
            <EventTrigger.Actions>
                <BeginStoryboard>
                    <Storyboard RepeatBehavior="Forever" AutoReverse="True">
                        <DoubleAnimation To="185" Duration="0:0:9"
Storyboard.TargetName="button1"
Storyboard.TargetProperty="Height"/>
                        <DoubleAnimation To="185" Duration="0:0:9"
Storyboard.TargetName="button1"
Storyboard.TargetProperty="Width"/>
                    </Storyboard>
                </BeginStoryboard>
            </EventTrigger.Actions>
        </EventTrigger>
    </Grid.Triggers>
    <Button x:Name="button1" Height="425" Width="425" Content="Silverlight and ASP.NET" Background="DarkCyan" Foreground="Red" FontWeight="SemiBold" FontSize="15"/>
</Grid>
</UserControl>
```

5. Right-click the AnimatedButtonAppCSTestPage.aspx file in Solution Explorer and select the Set as Start Page option.

6. Run the AnimatedButtonAppCS application by pressing the F5 key on the keyboard. The output of the application appears, as shown in Figure 17.48:

![](img/e073a4882197be4ab61103cbe0bcb394_936_0.png)

Figure 17.48: Animated Button Implemented Through Silverlight in ASP.NET Web Application

## Data Binding with Silverlight Application

You can perform data binding in a Silverlight application also. A Silverlight application like an ASP.NET application can be displayed in the Web browser. Unlike Silverlight 1, Silverlight 2 has controls that support data-binding features. The data-binding capabilities of Silverlight offer more power and flexibility of data with less runtime code. For data binding in Silverlight, you can use the DataGrid control. Let’s create a Silverlight application to display data:

- 1. Create a Silverlight Application named DataBindinginSilverlightCS (available on the CD).
- 2. Click the OK button in the New Project dialog box. The New Silverlight Application dialog box opens (Figure 17.49).
- 3. Select the Host the Silverlight application in a new Web site check box for hosting the Silverlight content, in the New Silverlight Application dialog box.
- 4. Select Silverlight 3 in the drop-down list labeled Silverlight Version, and then click the OK button, as shown in Figure 17.49:

![](img/e073a4882197be4ab61103cbe0bcb394_937_0.png)

Figure 17.49: Specifying a Host for a Silverlight Application

This creates two projects in your application named DataBindinginSilverlightCS and DataBindinginSilverlightCS.Web. The first project, DataBindinginSilverlightCS is the Silverlight application. The second project, DataBindinginSilverlightCS.Web is created for you as a test environment for the Silverlight project.

- 5. Create a connection to the Employees table in the Northwind database from the Server Explorer window. The Server Explorer window, if not already open, can be opened by selecting the View→Server Explorer menu bar option. After creating the connection, you need to create the Web service.
- 6. Right-click the test project, DataBindinginSilverlightCS.Web, and select the Add → New Item option for creating a WCF service, as shown in Figure 17.50:
