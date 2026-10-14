![](bbox=[0.09, 0.06, 0.91, 0.65])

10. Click OK.

The Object Collection Editor closes. If you examine the XAML markup for the title ComboBox, it should now look like this:

Click here to view code image

```
<ComboBox x:Name="title" HorizontalAlignment="Left"
Margin="420,240,0,0"
    VerticalAlignment="Top" Width="100" FontSize="20"/>
    <ComboBoxItem Content="Mr"/>
</ComboBox>
```

There are two things to notice here. The first is that the ComboBox markup has been split into an opening <ComboBox> tag and a closing </ComboBox> tag. The second is that between these tags, Visual Studio has added a ComboBoxItem element with the Content property set to Mr. This