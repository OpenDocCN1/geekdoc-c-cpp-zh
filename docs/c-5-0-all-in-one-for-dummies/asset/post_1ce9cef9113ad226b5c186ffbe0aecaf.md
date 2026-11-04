
```
NotifyPropertyChanged("Make");
}
}
public string Model
{
    get { return _model; }
    set
    {
        if (_model != value)
        {
            _model = value;
            NotifyPropertyChanged("Model");
        }
    }
}
```

## 11. Run the application again.

Now when you click the Change Data Context Value with Code-Behind button, the changed values get reflected automatically in the TextBox elements. This is due to the combination of the TwoWay binding mode as well as the implementation of INotifyPropertyChanged. (See Figure 3-3.)

![](img/80ff26f06fc9ab951e1cd4257b867366_635_0.png)

Figure 3-3:
TwoWay Data Binding with INotifyPropertyChanged.

## Validating data

It's good practice to validate any input provided to you from the user. People aren't perfect, and some people can be downright malicious. WPF provides a built-in framework for data validation and error notification. It's available to you through the implementation of the IDataErrorInfo interface on your classes.

You can add validation to the Car class you already created in Binding Sample2 from the preceding section.

## Element binding

In this chapter, you bind Label and TextBox controls to properties of underlying objects. You're not limited to this scenario; you can bind to just about anything from primitive variables to property values gleaned from other UIElements. Element binding in particular has its own component in the Binding expression. For instance, suppose that you have a TextBox and Label control in your window. You'd like to have the Content of the Label automatically update with the changing value of the Text property of the TextBox. The XAML code to accomplish Element Binding between the TextBox and the Label looks similar to

```
<Label x:Name="lblCarMake"
    Content="{Binding
        ElementName=txtCarMake,
        Path=Text}">
    <TextBox x:Name="txtCarMake"
        Width=200 Height=25 />
```

The C# code to define this binding looks similar to

```
Binding b = new
Binding("Text");
b.ElementName = "txtCarMake";
BindingOperations.
SetBinding(lblCarMake, Label.
ContentProperty, b);
```

![](img/80ff26f06fc9ab951e1cd4257b867366_636_0.png)

The complete solution is available on the web in the BindingSample2-Validation project.

Just follow these steps to add validation to your Car class:

- 1. Open the Car.cs file and edit the class to also implement the IDataErrorInfo interface, like this:

```
public class Car : INotifyPropertyChanged, IDataErrorInfo
```

Implementing this interface adds the following methods to the Car class:

```
public string Error
{
    get { throw new NotImplementedException(); }
}

public string this[string columnName]
{
    get { throw new NotImplementedException(); }
}
```

- 2. Edit the Get method of the Error property to return null.

Now it's time to add some validation rules to the properties of the Car object. The Car Make and Model properties should enforce the rule that they must always be at least three characters in length. The public string this[string columnName] method is used by the DataBinding engine to validate the properties of the object as they are changed, based on the name of the property (which is what they mean by columnName in the method signature). This method returns any error messages related to the property being edited.

3. To define and enforce these rules, edit the public string this[string columnName] method like this:

```
public string this[string columnName]
{
    get {
        string retval = null;
        if (columnName == "Make")
        {
            if (String.IsNullOrEmpty(this._make)
                || this._make.Length < 3)
            {
                retval = "Car Make must be at least 3 " +
                    "characters in length";
            }
        }
        if (columnName == "Model")
        {
            if (String.IsNullOrEmpty(this._model)
                || this._model.Length < 3)
            {
                retval = "Car Model must be at least 3 " +
                    "characters in length";
            }
        }
        return retval;
    }
}
```

In MainWindow.xaml, the Make and Model properties are bound to TextBox controls in the user interface.

4. To enable the text being entered into the TextBoxes to be validated against the constraints defined on the underlying property, edit the binding expressions in each TextBox like this:

```
<TextBox x:Name="txtCarMake" VerticalAlignment="Top"
Text="{Binding Path=Make, Mode=TwoWay,
UpdateSourceTrigger=PropertyChanged,
ValidatesOnDataErrors=True,
ValidatesOnExceptions=True}"
Width="200" Height="25" />

<TextBox x:Name="txtCarModel" VerticalAlignment="Top"
Text="{Binding Path=Model, Mode=TwoWay,
UpdateSourceTrigger=PropertyChanged,
ValidatesOnDataErrors=True,
ValidatesOnExceptions=True}"
Width="200" Height="25" />
```

UpdateSourceTrigger identifies when the validation calls take place. In this example, validations occur as the text is changing, and is fired off when the underlying object property fires the PropertyChanged event.

ValidatesOnDataErrors is what enables the IDataErrorInfo validation method to be called on the property.

![](img/80ff26f06fc9ab951e1cd4257b867366_637_0.png)

ValidatesOnExceptions will invalidate the TextBox if the underlying data source throws an exception, like when, for instance, you have an integer property and the user enters a string — WPF automatically throws the exception that the input string was not in the correct format.

5. Run the Sample and remove all text from the Make and Model TextBox controls.

You see that the TextBox controls are now rendered in red: as you enter text back into the TextBox, as soon as you reach three characters, the red stroke disappears. Figure 3-4 shows the Make text box in an invalid state.

Figure 3-4:
Simple Data Validation using the IDataErrorInfo interface.

![](img/80ff26f06fc9ab951e1cd4257b867366_638_0.png)

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

```
Style="{StaticResource ResourceKey=errorAwareTextBox}"
```

Now when you run the application and remove the text out of the TextBox controls, the TextBox displays a tooltip with the actual error message. (See Figure 3-5.)

![](img/80ff26f06fc9ab951e1cd4257b867366_639_0.png)

Figure 3-5:
Displaying error messages using Styles.

## Converting your data

WPF provides you the capability to cater your user interface to be intuitive for the user. Sometimes this means allowing them to enter data in different formats that make sense to them, giving you the responsibility of translating their data entry into a format allowable by your data source. The same is true vice versa; you want to translate data from your data source into a more intuitive form for the user. A popular use-case for this type of conversion is the string representation of a date value, or if you want to display a red or green circle instead of the values True or False.

WPF makes converting data easy by providing a simple interface to implement called IValueConverter. This interface contains two methods:

- ♦ **Convert:** This method obtains values from the data source and molds them to the form to be displayed to the user onscreen.
- ♦ **ConvertBack:** This method does the opposite — it takes the value from the user interface and molds it into a form that the data source expects.

It is important to note that with these methods, you're not held to the same data type as the value being bound. For instance, your data source property being bound can be a Date data type, and the Convert method can still return a string value to the user interface.

To demonstrate this feature, create a new WPF application project called BindingSample3. This project is a dashboard application that can show
