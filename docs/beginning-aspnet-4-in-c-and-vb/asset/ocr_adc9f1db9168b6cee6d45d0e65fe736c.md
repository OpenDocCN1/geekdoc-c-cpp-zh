In the constructor of the MainWindow class, a new object of the class SomeData is initialized and passed to the DataContext for data binding:

```
public partial class MainWindow: Window
{
    private SomeData p1 = new SomeData { Value1 = 11 };

    public MainWindow()
    {
        InitializeComponent();
        this.DataContext = p1;
    }
}
```

code snippet ValidationDemo/MainWindow.xaml.cs

The event handler method OnShowValue displays a message box to show the actual value of the SomeData instance:

```
private void OnShowValue(object sender, RoutedEventArgs e)
{
    MessageBox.Show(p1.Value1.ToString());
}
```

With simple data binding, here the Text property of a TextBox is bound to the Value1 property. If you run the application now and try to change the value to one that is not valid, you can verify that the value never changed by clicking the Submit button. WPF catches and ignores the exception thrown by the set accessor of the property Value1:

```
<Label Margin="5" Grid.Row="0" Grid.Column="0">Value1:</Label>
<TextBox Margin="5" Grid.Row="0" Grid.Column="1" Text="{Binding Path=Value1}" />
```

code snippet ValidationDemo/MainWindow.xaml

To display an error as soon as the context of the input changes, you can set the ValidatesOnException property of the Binding markup extension to True. With an invalid value (as soon as the exception is thrown when the value should be set), the TextBox is surrounded by a red line, as shown in Figure 36-11.

```
<Label Margin="5" Grid.Row="0" Grid.Column="0">Value1:</Label>
<TextBox Margin="5" Grid.Row="0" Grid.Column="1" Text="{Binding Path=Value1, ValidatesOnExceptions=True}" />
```

![](bbox=[0.78, 0.6, 0.94, 0.78])

To return the error information in a different way to the user, you can assign the attached property ErrorTemplate that is defined by the Validation class to a template defining the UI for errors. The new template to mark the error is shown here with the key validationTemplate. The ControlTemplate puts a red exclamation point in front of the existing control content:

```
<ControlTemplate x:Key="validationTemplate">
    <DockPanel>
        <TextBlock Foreground="Red" FontSize="20">!</TextBlock>
        <AdornedElementPlaceholder/>
    </DockPanel>
</ControlTemplate>
```

Setting the validationTemplate with the Validation.ErrorTemplate attached property activates the template with the TextBox:

```
<Label Margin="5" Grid.Row="0" Grid.Column="0">Value1:</Label>
<TextBox Margin="5" Grid.Row="0" Grid.Column="1" Text="{Binding Path=Value1, ValidatesOnExceptions=True}" Validation.ErrorTemplate="{StaticResource validationTemplate}" />
```

The new look of the application is shown in Figure 36-12.

![](bbox=[0.78, 0.82, 0.94, 0.98])