The Width property specifies the width of the control, and the TextWrapping property indicates what happens if the user attempts to enter information into the control that exceeds its width. In this case, all the TextBox controls wrap the text onto another line of the same width (the control will expand vertically). The alternative value, NoWrap, causes the text to scroll horizontally as the user enters it.

+   9. Add a ComboBox to the form, placing it below the Title TextBlock control, between the id and firstName TextBox controls. Set the properties of this control as follows:

| Property | Value |
| --- | --- |
| x:Name | title |
| HorizontalAlignment | Left |
| Margin | 420,240,0,0 |
| VerticalAlignment | Top |
| Width | 100 |
| FontSize | 20 |

The equivalent XAML markup for this control is as follows:

Click here to view code image

```
<ComboBox x:Name="title" HorizontalAlignment="Left"
Margin="420,240,0,0"
VerticalAlignment="Top" Width="100" FontSize="20"/>
```

You use a ComboBox to display a list of values from which the user can select.

+   10. In the XAML markup, replace the definition of the ComboBox control and add four ComboBoxItem controls, as follows in bold:

Click here to view code image

```
<ComboBox x:Name="title" HorizontalAlignment="Left"
Margin="420,240,0,0"
VerticalAlignment="Top" Width="75" FontSize="20">
```