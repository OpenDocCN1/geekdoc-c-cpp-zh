ValidatesOnExceptions will invalidate the TextBox if the underlying data source throws an exception, like when, for instance, you have an integer property and the user enters a string — WPF automatically throws the exception that the input string was not in the correct format.

5. Run the Sample and remove all text from the Make and Model TextBox controls.

You see that the TextBox controls are now rendered in red: as you enter text back into the TextBox, as soon as you reach three characters, the red stroke disappears. Figure 3-4 shows the Make text box in an invalid state.

Figure 3-4:
Simple Data Validation using the IDataErrorInfo interface.

![](bbox=[0.22, 0.42, 0.62, 0.7])

The red stroke is sufficient to indicate that an error has occurred, but it's of little use to the users as they're not informed of the details of the error. A simple way to display the error is to add a tooltip on the TextBox. Do this by adding a Style resource to your Window that defines a style that will trigger the tooltip when the data is in an invalid state.

6. Add the following XAML directly below the Window tag at the top of MainWindow.xaml, like this:

```
<Window.Resources>
    <Style x:Key="errorAwareTextBox" TargetType="{x:Type TextBox}">
        <Style.Triggers>
            <Trigger Property="Validation.HasError" Value="true">
                <Setter Property="ToolTip" Value="{Binding RelativeSource={x:Static RelativeSource.Self}, Path=(Validation.Errors)[0].ErrorContent}"/>
            </Trigger>
        </Style.Triggers>
    </Style>
</Window.Resources>
```

7. Add a Style attribute to your TextBox Style, like this: