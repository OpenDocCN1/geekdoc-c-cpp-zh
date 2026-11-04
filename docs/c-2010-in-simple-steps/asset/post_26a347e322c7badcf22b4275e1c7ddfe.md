
## Using the Path Property

You can also use the **Path** property to specify the source value that you want to bind in a WPF application. The **Path** property is the name of the property of the source object used for binding. For example, you can bind the **Text** property of the **TextBox** control. You can also bind an attached property of a control by using the **Path** property. For example, the following syntax is used with the **Path** property to bind the attached property, **DockPanel.Dock**:

```
Path = {DockPanel.Dock}
```

You can also bind the property of a control to a particular field of a database by using the **Path** property, as shown in the following syntax:

```
Path=Employees.FirstName
```

In the preceding syntax, the control is bound to the **FirstName** column of the **Employees** table.

Let's now perform data binding in a WPF application by using the **Path** property:

- 1. Open the WPF application named **WPFDataBinding**.
- 2. Add a new window to the **WPFDataBinding** application by right-clicking the application name in **Solution Explorer** and selecting **Add ➤ Window** from the context menu. A window named **Window2.xaml** is added to the application.
- 3. Set the title of the **Window2** window to **Binding using the Path Property** by using the **Title** property.
- 4. Add the highlighted code given in Listing 8.9 to the **Window2.xaml** file.

Listing 8.9: Creating Data Binding by using the Path Property

```xml
<Window x:Class="WPFDataBinding.Window2"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="Binding using the Path Property " Height="222" Width="300" Loaded="window_Loaded">
    <Grid Name="grid" DataContext="{Binding ElementName=mcListBox, Path=SelectedItem}">
        <TextBox Margin="10,10,10,121" FontWeight="Bold">Pick a color from below list
        </TextBox>
        <ListBox Name="mcListBox" Height="100" Width="100"
                 Margin="28,46,0,0" HorizontalAlignment="Left" VerticalAlignment="Top">
            <ListBoxItem>Orange</ListBoxItem>
            <ListBoxItem>Green</ListBoxItem>
            <ListBoxItem>Blue</ListBoxItem>
            <ListBoxItem>Gray</ListBoxItem>
            <ListBoxItem>LightGray</ListBoxItem>
            <ListBoxItem>Red</ListBoxItem>
        </ListBox>
        <Ellipse Height="100" Name="ellipse1" DataContext="{Binding
            ElementName=mcListBox}" Stroke="Black" Margin="0,46,31,0"
            VerticalAlignment="Top" HorizontalAlignment="Right" Width="116">
            <Ellipse.Fill>
                <Binding Path="SelectedItem.Content"/>
            </Ellipse.Fill>
        </Ellipse>
    </Grid>
</Window>
```

In Listing 8.9, the highlighted code indicates that the **Binding** property is used to bind an **Ellipse** control's **Fill** property to a **ListBox** control's selected value. In the code, notice that the **DataContext** attribute for the **Ellipse** control is set to the binding definition. The **Binding** property of the **Ellipse** control sets the binding for the control to the **ListBox** control by specifying the ID of the control in the **ElementName** property. The value of the selected item in the **ListBox** is assigned to the **Ellipse** control by using the **Path** property.

- 5. Set **Window2** window as the startup object.
- 6. Press the **F5** key to execute the **WPFDataBinding** application. The output appears.
- 7. Click the **Blue** color option in the list box. The output appears, as shown in Fig.C8.33:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_289_0.png)

In Fig.C8.33, the ellipse is filled with blue color, when the **Blue** option is selected in the list box. Next, let's learn about data binding on binding sources, such as CLR and ADO.NET objects.

## Binding Sources in WPF

In data binding, the source refers to the object that you obtain data from. WPF supports the CLR and ADO.NET data object binding sources. For the CLR object, data binding works as long as the binding engine is able to access the source property by using reflection. For ADO.NET object, you must establish a connection with the SQL Server database.

> **Note**
>
> .NET Framework facilitates you to obtain information (such as data type) about an existing variable in an application by using reflection. For instance, you can use the GetType() method to know about the data type of a variable used in an application. You can also use reflection to access the properties or invoke the methods of an existing object by using reflection in .NET applications.

Next, let's learn how to bind to CLR objects in WPF applications.

## Binding to CLR Objects

In WPF, you can bind to the public properties or subproperties of any CLR object. The binding object in WPF uses CLR reflection to retrieve the values of the properties. When you use the CLR object for data binding in WPF, you should implement the **INotifyPropertyChanged** interface. This interface helps you to update the binding target when the binding source property changes. This helps to ensure that the data used in the binding stays current.

If the source object implements a proper notification mechanism, the target updates happen automatically. You can also use the **UpdateTarget()** method to update the target property to provide property change notification. Now, let's learn how to implement CLR object binding in a WPF application. For this, perform the following steps:

- 1. Create a WPF application named **BindingtoCLRObject**.
- 2. Set the title of the **MainWindow** window to **Binding to a CLR Object** by using the **Title** property.
- 3. Add the highlighted code given in Listing 8.10 to the **MainWindow.xaml** file:

**Listing 8.10:** Preparing the User Interface of the MainWindow.xaml File

```xml
<Window x:Class="BindingtoCLRObject.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="Binding to a CLR Object" Height="300" Width="300">
    <Grid Name="grdMain">
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="30" />
            <ColumnDefinition Width="70" />
        </Grid.ColumnDefinitions>
```

```xml
<Grid.RowDefinitions>
    <RowDefinition Height="50" />
    <RowDefinition Height="50" />
    <RowDefinition Height="50" />
    <RowDefinition Height="50" />
    <RowDefinition Height="50" />
</Grid.RowDefinitions>
<Label Grid.Column="0" Grid.Row="0" Name="...">Name:</Label>
<TextBox Width="200" Height="30" Grid.Column="1" Grid.Row="0"
    Text="{Binding Name}" />
<Label Grid.Column="0" Grid.Row="1">Age:</Label>
<TextBox Width="200" Height="30" Grid.Column="1" Grid.Row="1"
    Text="{Binding Age}" />
<Label Grid.Column="0" Grid.Row="2">Profile:</Label>
<TextBox Width="200" Height="30" Grid.Column="1" Grid.Row="2"
    Text="{Binding Profile}" />
<Label Grid.Column="0" Grid.Row="3">EmployeeID:</Label>
<TextBox Width="200" Height="30" Grid.Column="1" Grid.Row="3"
    Text="{Binding EmployeeID}" />
<Button Margin="5,5,5,5" Grid.Column="1" Grid.Row="4" Name="Button"
    Click="Button_Click" ShowData="...">Show Data</Button>
</Grid>
</Window>
```

After adding the preceding code to the *MainWindow.xaml* file, you need to add a class to your application. For this, proceed to the next step.

- 4. Right-click the application name in *Solution Explorer* and select *Add→Class* from the context menu, as shown in Fig.C8.34.

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_290_0.png)

The Add New Item dialog box appears.

- 5. Enter the name *Data.cs* in the *Name* text box.
- 6. Click the *Add* button to add the *Data.cs* file to the application.
- 7. Add the highlighted code given in Listing 8.11 to the *Data.cs* file:

Listing 8.11: Showing the Code to Add in the *Data.cs* File

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace BindingtoCLRObject
{
    class Data
    {
        public Data(string name, string age, string profile, string id)
```
