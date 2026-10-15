
```csharp
get { return _state; }
set { _state = value; }
}
public Place(string name, string state)
{
    this._name = name;
    this._state = state;
}
}
public class Places : ObservableCollection<Place>
{
    public Places()
    {
        Add(new Place("India", "INDIA"));
        Add(new Place("Australia", "AUS"));
        Add(new Place("America", "USA"));
        Add(new Place("Africa", "AFR"));
        Add(new Place("Russia", "USSR"));
    }
}
}
```

The preceding code binds the data to the window. You can run the application by pressing the F5 key. The output of Listing 10.31 and Listing 10.32 appears, as shown in Figure 10.61:

![](img/e073a4882197be4ab61103cbe0bcb394_490_0.png)

## Figure 10.61: Output using a Trigger

In Listing 10.31 and Listing 10.32, the DataTrigger trigger is specified in such a way that if the state is INDIA, then the forecolor of the corresponding item in the ListBox control is set to red.

## Using WPF Commands with Controls

One of the simplest ways to use a command in WPF is to use the predefined RoutedCommand class. The Cut, Copy, and Paste are predefined commands in the ApplicationCommand class. The MenuItem control has native support for invoking commands. Create a WPF application named WPFCommands_with_Controls (available in the CD) and add the following code to the MainWindow.xaml file, as shown in Listing 10.33:

### Listing 10.33: Showing the Code for Using WPF Command with Control

```
```xml
<Window x:Class="WPFCommands_with_Controls.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MainWindow" Height="350" Width="525">
    <Grid>
        <StackPanel>
            <Menu>
```

```
<MenuItem Command="ApplicationCommands.Paste" />
<MenuItem Command="ApplicationCommands.Copy" />
<MenuItem Command="ApplicationCommands.Cut" />
</Menu>
<TextBox Name="TextBox1"/>
<TextBox Name="TextBox2"/>
</StackPanel>
</Grid>
</window>
```

In Listing 10.33, three MenuItem controls with the Cut, Copy, and Paste commands and two TextBox controls are added. You can type text in one TextBox control and perform the Cut and Paste or Copy and Paste command in the other TextBox control. For example, as you type text in TextBox1 text box, the Cut and Copy commands are disabled. After you type the text and select it, the Cut and Copy commands are enabled. When you run the application, the TextBox control appears blank. When you perform some action on the Text control, you get the output as shown in Figure 10.62:

![](img/e073a4882197be4ab61103cbe0bcb394_491_0.png)

Figure 10.62: Using WPF Commands with Controls

## Hosting a Windows Forms Controls in a WPF Application

In WPF, you can integrate the controls of Windows Forms in a WPF application. You need a wrapper, which WPF control to host a Windows Forms control. This wrapper is a WindowsFormsHost class and is in WindowsFormsIntegration.dll assembly. The WindowsFormsHost class is derived from the base class HwndHost and FrameworkElement, and so can be used as a WPF element. There are some controls in Windows Forms, which are not available in the WPF application. You can add them by hosting a Windows Forms control in a WPF application. Some of these controls are MaskedTextBox, DateTimePicker, MonthCalendar, DataGridView, and PrintPreviewControl. Let’s learn to host a Windows Forms control in a WPF application by performing the following steps:

- 1. Create a WPF application named WindowsForms_in_WPFApplication (available in the CD).
- 2. Add a reference to the WindowsFormsIntegration assembly, which is named WindowsFormsIntegration.dll in the Solution Explorer. Then, add a reference to Windows Forms assembly, which is named System.Windows.Forms.dll.
- 3. Add the code in the MainWindow.xaml file, as shown in Listing 10.34:

### Listing 10.34: Showing the Code for Using Windows Forms Control in WPF Application

```
<window x:Class="WindowsForms_in_WPFApplication.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:wf="clr-namespace:System.Windows.Forms;assembly=System.Windows.Forms"
Title="HostingwfInwpf" Height="191" Width="182">
<Grid Height="108" Width="127">
<windowsFormsHost>
<wf:MaskedTextBox x:Name="Date" Mask="0000/00/00" />
</windowsFormsHost>
</Grid>
</window>
```

In the preceding code, the MaskedTextBox control is added as a child of the WindowsFormsHost control. You can run the application by pressing the F5 key.
The output of Listing 10.34 with the date entered in it is shown in Figure 10.63:

![](img/e073a4882197be4ab61103cbe0bcb394_492_0.png)

Figure 10.63: Displaying a Windows Forms Control in a WPF Application

## Hosting a WPF Control in a Windows Forms Application

Similar to the preceding example where a Windows Forms control is hosted in a WPF application, you can also host a WPF control in a Windows Forms application. However, you cannot use a WPF control in a Windows Forms application directly. You need to use the wrapper class, named ElementHost, from the System.Windows.Forms.Control namespace, to use the WPF control in the Windows Forms applications. The ElementHost control manages the WPF controls.

Let's learn to host a WPF control in a Windows Forms application by performing the following steps:

- 1. Create a Windows Forms application named WPFControl_in_WindowsForm (available in the CD) You get a blank Windows Form.
- 2. Right-click the project name and select Add→New Item in Solution Explorer.
- 3. Select the User Control (WPF) template in the Add New Item dialog box, provide the name, UserControl1.xaml, and click the Add button to add the User Control in the application.
- After the User Control is added to your Windows Forms application, you get an interface similar to that of a WPF application. You can add the WPF controls you need to the new WPF User Control.
- 4. Add a reference of the System.Xaml.dll assembly to the project.
- 5. Add the code, shown in Listing 10.35, in the UserControl1.xaml file:
- 6. Build the application by selecting Build→Build Solution from the menu bar.
- 7. Add an ElementHost control by dragging it from the WPF Interoperability tab of the Toolbox and dropping it on the Windows Form. The ElementHost control is used to place the WPF User Control on the form.

### Listing 10.35: Showing the Code for Adding a WPF Control to a Windows Forms Application

```
<UserControl x:Class="WPFControl_in_WindowsForm.UserControl1"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    mc:Ignorable="d"
    d:DesignHeight="300" d:DesignWidth="300">

    <Grid>
        <Ellipse Margin="76,40,91,136" Name="ellipse1" Stroke="White" StrokeThickness="4" Fill="LightBlue"/>
        <Rectangle Margin="15,0,10,27" Name="rectangle1" Stroke="white" Height="110" VerticalAlignment="Bottom" StrokeThickness="4" Fill="Pink"/>
    </Grid>
</UserControl>
```

8. Click the arrow in the top-right corner to display a Smart Tag, to select the content for the ElementHost control, as show in Figure 10.64:

![](img/e073a4882197be4ab61103cbe0bcb394_493_0.png)

9. Select UserControl1 in the Select Hosted Content drop-down list of the Smart Tag.

The WPF application created by you in the UserControl1.xaml file appears inside the ElementHost control.

10. Run the application by pressing the F5 key. The output of the application appears, as shown in Figure 10.65:

![](img/e073a4882197be4ab61103cbe0bcb394_493_1.png)

Now, let’s recapitulate the main topics discussed in this chapter.

## Summary

In this chapter, you have learned about various controls of WPF that are used to create a WPF application. You have also learned about the resources, styles, templates, and triggers used in WPF. The chapter also discussed resources in WPF that help you to define the commonly-used values in your application at one place and reuse them. Next, you learned about styles, templates, and triggers to be used in a WPF application. You have also learned about WPF commands that help you to perform additional operations on your application, such as Cut, Copy, and Paste.

In the next chapter, you learn to work with the Typography and Documents features in WPF.
