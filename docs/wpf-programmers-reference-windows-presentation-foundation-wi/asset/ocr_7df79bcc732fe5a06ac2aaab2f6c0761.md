The code starts with a GroupBox that displays the header "Appointment Info." The GroupBox contains a StackPanel that holds a CheckBox and the WindowsFormsHost. The WindowsFormsHost’s Child property contains a DateTimePicker control.

Figure 6-15 shows the result.

The program uses the following C# code-enable the DateTimePicker only when the CheckBox is checked. When the control is enabled, you can click on it to change the month, date, and year, or you can click on the dropdown arrow to display the month selection area shown in Figure 6-15.

![](bbox=[0.595, 0.065, 0.865, 0.275])

FIGURE 6-15

```
// Enable the DateTimePicker so the user can make an appointment.
private void chkMakeAppointment_Checked(object sender, RoutedEventArgs e)
{
    dtpAppointment.Enabled = true;
}
```

```
// Disable the DateTimePicker.
private void chkMakeAppointment_Unchecked(object sender, RoutedEventArgs e)
{
    dtpAppointment.Enabled = false;
}
```

UseWindowsFormsHost

Before you can use a WindowsFormsHost, you must perform three steps:

+   1. Add a reference to the WindowsFormsIntegration library. In Visual Studio, you can open the Project menu, select "Add Reference," and select the library from the NET tab on the Add Reference dialog. In Expression Blend, you can open the Project menu, select Add Reference, and then browse to the library. On my system, it is installed at C:\Program Files\Microsoft\Framework\v3.0\WindowsFormsIntegration.dll.
2. Add a reference to the System.Windows.Forms.dll library. Again, in Visual Studio, you can use the Project menu Add Reference command and select the library from the resulting dialog. In Expression Blend, you can again use the Project menu Add Reference command and then browse to the library. On my system, it is installed at C:\Windows\Microsoft\.NET\Framework\v2.0.50727\System.Forms.dll.
3. Add a namespace declaration for the Windows namespace to the top of the XAML file. The declaration should look like this:
xmlms:wf="clr-namespace:System.Windows.Forms;assembly=System.Windows.Forms*"

This makes wf the abbreviation for the namespace, so you can refer to Windows Forms controls as wf:DateTimePicker.