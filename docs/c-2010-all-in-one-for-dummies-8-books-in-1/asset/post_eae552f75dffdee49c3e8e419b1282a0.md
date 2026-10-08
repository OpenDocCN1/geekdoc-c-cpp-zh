
# Editing, Validating, Converting, and Visualizing Your Data 589

## Element binding

In this chapter, we bind Label and TextBox controls to properties of underlying objects. You are not limited to this scenario; you bind to just anything about primitive variables to properties gleaned from other UIElements. Element binding in particular for example, suppose you have a TextBox and Label control in your window. You would have the Content automatically updating the changing value of the TextBox. The XML code to accomplish Element binding between the TextBox and the Label looks to:

```xml
<Label x:Name="lblCar" Content="(Binding Path=txtCar)" />
<TextBox x:Name="txtCar" Width="200" Height="25" />
```

The C# code to define this binding looks similar:

```csharp
Binding b = new Binding("Text");
b.ElementName = "txtCar";
BindingOperations.SetBinding(lblCar, Label.Content, b);
```

## Validating data

It is good to validate any input provided to you from the user. People aren't perfect, and some people can be downright mischievous. WPF provides a built-in framework for data validation and error notification. It is available to you through the implementation of the IDataErrorInfo interface on surfaces.

Just add validation to the Car class you have already created in BindingSample2 from the preceding section.

The complete solution is available on the Web in the BindingSample2 Validation project.

Just follow these steps to add validation to your Car class:

- 1. Open the Car.cs file, and edit the class to also implement the IDataErrorInfo interface, like this:

```csharp
public class Car : INotifyPropertyChanged, IDataErrorInfo
{
    public string Error
    {
        get { throw new NotImplementedException(); }
    }
}
```

Implementing this interface adds the following methods to the Car class:

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_614_0.png)

```csharp
public string this[string columnName]
{
    get { throw new NotImplementedException(); }
}
```

- 2. Edit the Get method of the Error property to return null.

Now it's time to add some validation rules to the properties of the Car object. The Car and Model properties should enforce the rule that must always be at least three characters in length. The public string this[string columnName] method is used by the DataBinding engine to validate the properties of the object as they are changed, based on the name of the property (which is what they mean by columnName). This method returns an error message related to the property being edited.

- 3. To define and enforce these rules, edit the public string this[string columnName] method like this:

```csharp
public string this[string columnName]
{
    string returnValue = null;
    if (columnName == "Make")
    {
        if (String.IsNullOrEmpty(this.make) || this.make.Length < 3)
        {
            returnValue = "Car Make must be at least 3 characters in length";
        }
    }
    if (columnName == "Model")
    {
        if (String.IsNullOrEmpty(this.model) || this.model.Length < 3)
        {
            returnValue = "Car Model must be at least 3 characters in length";
        }
    }
    return returnValue;
}
```

- 4. In MainWindow.xaml, the Make and Model properties are bound to TextBox controls in the user interface. To enable the text being entered into the TextBoxes to be validated against the constraints defined on the underlying property, edit the binding expressions in each TextBox like this:

```xml
<TextBox x:Name="TextCarMake" VerticalAlignment="Top" Text="{Binding Path=Make, Mode=TwoWay, UpdateSource=PropertyChanged, ValidatesOnDataErrors=True, ValidatesOnExceptions=True}" Width="200" Height="25" />

<TextBox x:Name="txtCarModel" VerticalAlignment="Top" Text="{Binding Path=Model, Mode=TwoWay, UpdateSourceTrigger=PropertyChanged, ValidatesOnDataErrors=True, ValidatesOnExceptions=True}" Width="200" Height="25" />
```

UpdateSourceTrigger identifies when the validation calls take place. In this example, validations occur as the text is changing, and is fired off when the underlying object fires the PropertyChanged event.

ValidatesOnDataErrors enables what the IDataErrorInfo validation method to be called on the property.

ValidatesOnExceptions will invalidate the TextBox if the underlying data source throws an exception, like, when you have an integer property and the user enters a string — WPF automatically throws the exception that the input string was not in the correct format.

- 5. Run the Sample, and remove all text from the Make and Model TextBox controls. You will see the TextBox controls are now rendered in red; as you enter text back into the TextBox, as soon as you reach three characters, the red stroke disappears. Figure 3-4 shows the Make box text in an invalid state.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_616_0.png)

Figure 3-4: Simple Validation using the IDataErrorInfo interface.

- 6. The red stroke is sufficient enough to indicate that an error has occurred, but it's of little use to the users as they are not informed of the details of the error. A simple way to display the error is to add a tooltip on the TextBox. Do this by adding a Style resource to a Window that defines a style that will trigger the tooltip when the data is in an invalid state. Add the following XAML directly below the Window tag at the top of MainWindow.xml, like this.

```xml
<Window.Resources>
  <Style x:Key="errorAwareTextBox" TargetType=(x:Type TextBox)">
    <Style.Triggers>
      <Trigger Property="Validation.HasError" Value="true">
        <Setter Property="ToolTip"
            Value="{Binding RelativeSource={x:Static RelativeSource}, Path=(Validation.Errors)[0].Content}" />
      </Trigger>
    </Style.Triggers>
  </Style>
</Window.Resources>
```

- 7. Add a Style attribute to your TextBox Style, like this: `Style="{StaticResource errorAwareTextBox}"`. Now when you apply the attribute and remove the text from the TextBox, the TextBox displays a tooltip with the actual error message ![](img/36596fb11aa4233d5cab0d6ddd1d82e8_617_png) Figure 3-5: Displaying error messages using Styles.

WPF provides the capability to translate data into different formats. This sometimes means allowing them to enter data that makes sense to the user, or versa. It is important to note that with these methods you are not held to data type. For instance, create a new WPF application called BindingSample3. This is a dashboard application that can show the status of servers. In project you implement two controls, RedX and GreenCheck. You also create a value converter that converts a Boolean value to color.

Follow these steps to create:

1. Create a new WPF application named BindingSample3.
2. Add a new User Control to GreenCheck.xaml.
3. Replace the XAML found in GreenCheck.xaml with this XAML:

```xml
<UserControl x:Class="BindingSample3.GreenCheck"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:mc="http://schemas.microsoft.com/expression/markupcompatibility="2006"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
d:DesignHeight="50" d:DesignWidth="50">
<Canvas x:Name="CheckCanvas" Width="50.4845" Height="49.6377"
Canvas.Left="0" Top="0">
<Path x:Name="Checkpath" Width="43.4167" Height="45.6667"
Canvas.Left="0" Top="1.3113-e-06"
Stroke="Fill" Fill="#FF006432"
Data="M 19.0833,45.6667 41.3667,2.461627,2..338
1.3113-e-06 19.0833,42.5833 2.461627,25.3333
0,
27.9167 17.4167,44.25"/>
</Canvas>
</UserControl>
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_618_0.png)
