# Binding to CLR Objects

In WPF, you can bind a control to the data by using the public properties or the sub-properties of any CLR object. The binding object in WPF uses CLR to retrieve the values of the properties. When you use the CLR object for data binding in WPF, you should implement the `INotifyPropertyChanged` interface. This interface helps you to update the target when the source property changes, thereby ensuring that the data used in binding process is current. You can also use the `UpdateTarget()` method to update the target property to provide the proper change notification.

Perform the following steps to implement CLR object binding by creating a Windows Forms application named **BindingtoCLRObject** (also available on the CD):

+   1. *Open* Microsoft Visual Studio 2010.
+   2. *Select* **File→New→Project** from the menu bar. The **New Project** dialog box appears.
+   3. *Select* Visual C#→**Windows** in the **Installed Templates** pane of the **New Project** dialog box.
+   4. *Select* **WPF Application** in the **middle** pane of the **New Project** dialog box.
+   5. *Enter* **BindingtoCLRObject** as the name of the application in the **Name** text box.
+   6. Enter the complete path where you want to save the application in the **Location** combo box.
+   7. *Click* the **OK** button in the **New Project** dialog box to close it. The **BindingtoCLRObject** application is created.
+   8. *Set* the title of **MainWindow** to **Binding to a CLR Object** by using the **Title** property.
+   9. *Add* the code, given in Listing 5.13, to the **MainWindow.xaml** file:

**Listing 5.13:** Creating the User Interface of the BindingtoCLRObject Application

```
```xml
<Window x:Class="BindingtoCLRObject.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Binding to a CLR Object" Height="300" Width="300">
    <Grid Name="myGrid" Margin="5,5,5,5">
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="30%" />
            <ColumnDefinition Width="70%" />
        </Grid.ColumnDefinitions>
        <Grid.RowDefinitions>
            <RowDefinition Height="50" />
            <RowDefinition Height="50" />
            <RowDefinition Height="50" />
            <RowDefinition Height="50" />
            <RowDefinition Height="50" />
        </Grid.RowDefinitions>
        <Label Grid.Column="0" Grid.Row="0">Name:</Label>
        <TextBox Width="200" Height="30" Grid.Column="1" Grid.Row="0">
            Text="{Binding Name}" />
        <Label Grid.Column="0" Grid.Row="1">Age:</Label>
        <TextBox Width="200" Height="30" Grid.Column="1" Grid.Row="1">
            Text="{Binding Age}" />
        <Label Grid.Column="0" Grid.Row="2">Profile:</Label>
        <TextBox Width="200" Height="30" Grid.Column="1" Grid.Row="2">
            Text="{Binding Profile}" />
        <Label Grid.Column="0" Grid.Row="3">EmployeeID:</Label>
        <TextBox Width="200" Height="30" Grid.Column="1" Grid.Row="3">
            Text="{Binding EmployeeID}" />
        <Button Margin="5,5,5,5" Grid.Column="1" Grid.Row="4"
                Name="Button" Click="Button_Click">SHOW DATA</Button>
    </Grid>
</Window>
```
```

After adding the code, given in Listing 5.13, to the **MainWindow.xaml** file, add a class to your application.

+   10. *Right-click* the application name in **Solution Explorer** and select **Add→Class** from the context menu to add a class, as shown in Fig.C#-5.27: