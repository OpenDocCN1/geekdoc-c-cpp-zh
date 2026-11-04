Table 7.13: Noteworthy Properties of DatePicker class

| Property | Description |
|---|---|
| SelectionMode | Retrieves or sets a value that indicates what kind of date selections are allowed in a DatePicker control. The default value for the SelectionMode property is SingleDate, which means that only one date can be selected. |

Let's create a standalone WPF application named DatePickerDemo to show the use the DatePicker control. For this, perform the following steps:

+   1. Repeat steps 1 to 3 as followed earlier while creating the GridDemo application in the Using the Grid Control section of this chapter.
+   2. Enter the name DatePickerDemo in the Name text box and specify an appropriate location for the application in the Location combo box.
+   3. Click the OK button. The DatePickerDemo application is created.

4. Add the highlighted code given in Listing 7.18, in the MainWindow.xaml file:

# Listing 7.18: Showing the Code to Add a DatePicker Control

```
```xml
<Window x:Class="DatePickerDemo.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="DatePickerDemo" Height="300" Width="300">
<Grid>
<DatePicker Height="25" HorizontalAlignment="Left" Margin="10,10,0,0" Name="datePicker1" VerticalAlignment="Top" Width="115"/>
</Grid>
</Window>
```
```

In Listing 7.18, a DatePicker control is added to a Grid control. The Width and Height properties of the DatePicker control are set while the Name property is used to uniquely identify the DatePicker control.

5. Add the highlighted code given in Listing 7.19 to the MainWindow.xaml.cs file:

# Listing 7.19: Adding Code for the DatePicker Control

```
```csharp
namespace DatePickerDemo
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
            datePicker1.SelectedDate = new DateTime(2010, 5, 1);
            datePicker1.DisplayDateStart = new DateTime(2010, 5, 1);
            datePicker1.DisplayDateEnd = new DateTime(2010, 5, 31);
            datePicker1.FirstDayOfWeek = DayOfWeek.Monday;
        }
    }
}
```
```

As you can see in Listing 7.19, the DisplayDate property of the DatePicker control is set to May 1, 2010. The last date to be displayed on the DatePicker control is May 31, 2010, because of the DisplayDateEnd property. In addition, Monday is assigned as the first day of the week, using the FirstDayOfWeek property of the control.