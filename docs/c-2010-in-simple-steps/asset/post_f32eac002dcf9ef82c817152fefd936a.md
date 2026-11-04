
keys **firstBrush** and **secondBrush** are defined. These two resources are used to set the **Background** property of three buttons (**button1, button2, and button3**). The **StaticResource** markup extension is used to set the **Background** property to the resource values.

- **5** *Press the F5 key to run the StaticResourcesDemo application. The output appears, as shown in Fig.C#-7.37.*

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_258_0.png)

**Fig.C#-7.37**

In **Fig.C#-7.37**, the three buttons, **button1, button2, and button3** are displayed whose **Background** property is set using a **StaticResource** markup extension.

Let's now learn about dynamic resources.

## Using a Dynamic Resource

When you use the **DynamicResource** markup extension, the resource is referred to as a dynamic resource. Compared to static resources, dynamic resources provide more flexibility and are useful in situations when you want to defer the assignment of a property value until run time, for instance, when you want to change the value of the resource at run time through user or system settings.

Unlike static resources that are looked up at the time of loading, dynamic resources are looked up only when they are used at run time. With dynamic resources, an expression is created for the requested resource. This expression is not evaluated until run time. When a dynamic resource is used at run time, the key of the requested resource is looked up in the resources of the element on which the property is being set. If the key is not found, then that key is looked up in the parent element and its resource dictionary up to the root element. If the key is still not found, then the application, theme, and system resources are looked up, in that order.

Let's create a standalone WPF application named **DynamicResourcesDemo** to show the use of dynamic resources. For this, perform the following steps:

- 1. *Repeat steps 1 to 3* as followed earlier while creating the **GridDemo** application in the *Using the Grid Control* section of this chapter.
- 2. *Enter the name* **DynamicResourcesDemo** *in the* **Name** *text box and specify an appropriate location for the application in the* **Location** *combo box.*
- 3. *Click the* **OK** *button. The* **DynamicResourcesDemo** *application is created.*
- 4. *Add the highlighted code given in Listing 7.21, in the* **MainWindow.xaml** *file.*

### Listing 7.21: Using a Dynamic Resource in XAML

```xml
<Window x:Class="DynamicResourcesDemo.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Demo-DynamicResources" Height="300" Width="300">
    <Window.Resources>
        <SolidColorBrush x:Key="firstBrush" Color="Lavender"/>
        <SolidColorBrush x:Key="secondBrush" Color="PowderBlue"/>
        <SolidColorBrush x:Key="thirdBrush" Color="Violet"/>
    </Window.Resources>
    <Grid Name="grid1" Background="{StaticResource firstBrush}">
<Button Name="button1" Height="100" Width="150" Margin="0,0,0,75" Content="Dynamic Button" BorderBrush="Black" BorderThickness="5" Background="{DynamicResource grid1.Background}"/>
<Button Name="button2" Height="25" Margin="0,185,100,0" Width="75" Content="Color1" Click="button2_Click" />
<Button Name="button3" Height="25" Margin="100,185,0,0" Width="75" Content="Color2" Click="button3_Click" />
</Grid>
</Window>
```

In Listing 7.21, you can see that the Window control has three SolidColorBrush resources with the keys firstBrush, secondBrush, and thirdBrush. The firstBrush resource is referenced in the Background property of the grid1 control as a static resource. The Background property of the grid1 control is then used as a dynamic resource in the button1 control. This implies that whenever the background of the grid1 control changes, the background of the button1 control also changes.

- 5 Double-click the Color1 button in the Design view to add the button's Click event handler in the MainWindow.xaml.cs file.

- 6 Now, add the following code snippet for the button2_Click event handler in the MainWindow class:

```
private void button2_Click(object sender, RoutedEventArgs e)
{
    grid1.Background = (Brush)this.FindResource("secondBrush");
}
```

In the preceding code snippet, in the button2_Click event handler, the background of the grid1 control is set to the value of the secondBrush resource by using the FindResource() method.

- 7 Switch to the MainWindow.xaml file and double-click the Color2 button in the Design view to add the button's Click event handler in the MainWindow.xaml.cs file.

- 8 Add the following code snippet for the button3_Click event handler in the MainWindow class:

```
private void button3_Click(object sender, RoutedEventArgs e)
{
    grid1.Background = (Brush)this.FindResource("thirdBrush");
}
```

In the preceding code snippet, the background of the grid1 control is set to the value of the thirdBrush resource in the button3_Click event handler.

- 9 Press the F5 key to run the DynamicResourcesDemo application. The output appears, as shown in Fig.C#-7.38:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_259_0.png)

Fig.C#-7.38

- 10 Click the Color1 button in the Demo-DynamicResources window, as shown in Fig.C#-7.39:

2 Enter the name StylesDemo in the Name text box and specify an appropriate location for the application in the Location combo box.

3 Click the OK button. The StylesDemo application is created.

4 Add the highlighted code given in Listing 7.22, in the MainWindow.xaml file:

### Listing 7.22: Using Styles as Resources

```xml
<Window x:Class="StylesDemo.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="Demo-Styles" Height="200" Width="300">
<Grid>
<Grid.Resources>
<Style x:Key="myButtonStyle">
<Setter Property="Button.Background" Value="Black"/>
<Setter Property="Button.Foreground" Value="White"/>
</Style>
</Grid.Resources>
<Button Name="button1" Style="{StaticResource myButtonStyle}" Margin="10,10,140,85"/>
<Button Name="button2" Style="{StaticResource myButtonStyle}" Margin="140,85,10,10"/>
</Grid>
</Window>
```

In Listing 7.22, the Resource property of the Grid control has a Style element with the key myButtonStyle. The Style element has two Setter elements that specify the values for the Background and Foreground properties of the buttons in the grid. The Style element is then referred to as a static resource in the Style property of the button1 and button2 controls. This implies that both the buttons in the grid have the same style.

- 5 Press the F5 key to run the StylesDemo application. The output appears, as shown in Fig.C#-7.41:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_261_0.png)

Fig.C#-7.41

With this, we come to the end of the chapter. Let's now recap the main points discussed in the chapter.

## Summary

In this chapter, you have learned about:

- Architecture of WPF 4.0
- Enhancements in WPF 4.0
- Different types of WPF 4.0 applications
- WPF 4.0 Designer
- The use of XAML in WPF
- Using common and new controls WPF applications
- Using resources and styles in WPF applications

## Chapter 8

## ADO.NET and Data Binding

**In this Chapter:**

- Exploring ADO.NET
- Types of Data Binding in Windows Forms
- Data Binding in WPF

The world of business is growing rapidly and so is the need to store data. Data, as you know, is a collection of facts, which is generally stored in a database in the form of tables. A database is a collection of tables, which are used to store large amounts of data (information) systematically in a computer. This stored information can be accessed from the database quickly and efficiently as and when required. Databases that are used to relate data in multiple tables are called relational databases. Some popular relational databases are SQL Server (where SQL stands for Structured Query Language Server), Oracle, and Microsoft Access.

Retrieving and manipulating data directly from a database requires the knowledge of basic SQL commands. Anyone who is not familiar with SQL commands will not be able to use the data stored in a database. Therefore, most business applications provide a user-friendly interface that helps to retrieve data from a database without having to write SQL commands. Microsoft ActiveX Data Objects.NET (ADO.NET) is a model used by .NET applications, which you use to communicate with the database directly to retrieve and manipulate data.

This chapter introduces you to ADO.NET. You also learn about the concept of data binding and the different types of data binding in Windows Forms and Windows Presentation Foundation (WPF).

Let's first explore ADO.NET in brief.

## Exploring ADO.NET

ADO.NET is the main data access technology that a .NET application uses. ADO.NET uses a disconnected data architecture, which means that the data you work with is just a copy of the data in the database. Microsoft chose disconnected data architecture for a number of reasons. In traditional client/server applications, you are connected to a database and you need to maintain this connection, while the application is running. However, maintaining such connections requires a lot of server resources. Therefore, when you migrate to the Internet, you should follow the disconnected data architecture, instead of maintaining direct and continuous connections with the server to reduce the load on servers.

Let's now discuss the improvements in the ADO.NET 4.0 Entity Framework and the components that constitute ADO.NET.

## Improvements in the ADO.NET 4.0 Entity Framework

With ADO.NET Entity Framework, programmers are able to develop data access applications by programming the applications against a conceptual application model rather than directly programming against a relational storage schema. The main objective behind this is to decrease the amount of code and maintenance that is generally required for data-oriented applications.

The new features and enhancements incorporated in ADO.NET 4.0 Entity Framework include the following:

- **Support for creating foreign keys in the conceptual data model:** Enables developers to create conceptual models wherein foreign key columns in the database correspond to scalar properties on entity types. The properties of any entity type that map to a single field in the data storage model are referred to as scalar properties.
- **Introduction of self-tracking entities for n-tier application development:** Refers to the use of self-tracking entities while working with n-tier applications. These self-tracking entities can generally record changes to scalar, complex, and navigation properties.

> **Note**
> An n-tier application is one, which is distributed among three or more independent computers in a distributed network. In the term n-tier, n refers to some number, such as a 3-tier. In a 3-tier application, the user interface is in the user's computer, the business logic is stored in a more centralized computer, and the needed data is stored in a database server or a computer that manages a database.

- **New methods for n-tier application development:** Refers to the new methods that have been added in the System.Data.Objects namespace to facilitate easier development of n-tier applications.
