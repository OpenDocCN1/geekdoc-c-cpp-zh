# 612 Editing, Validating, Converting, and Visualizing Your Data

by columnName in the method signature). This method returns any
error messages related to the property being edited.

+   3. To define and enforce these rules, edit the public string
this[columnName] method like this:

```
public string this[string columnName]
get
{
    string returnValue = null;
    if (columnName == "Make")
    {
        if (String.IsNullOrEmpty(this._make)
            || this._make.Length < 3)
        {
            returnValue = "Car Make must be at least 3 " * +
                "characters in length";
        }
    }
    if (columnName == "Model")
    {
        if (String.IsNullOrEmpty(this._model)
            || this._model.Length < 3)
        {
            returnValue = "Car Model must be at least 3 " * +
                "characters in length";
        }
    }
    return returnValue;
}
```

In MainWindow.xaml, the Make and Model properties are bound to
TextControls in the user interface.

+   4. To enable the text being entered into the TextBoxes to be validated
against the constraints on the underlying property, edit the
binding expressions in each TextBox like this:

```
<TextBox x:Name="txtCar" VerticalAlignment="Top"
    Binding Path=Make, Mode=TwoWay,
    UpdateSource=PropertyChanged,
    ValidatesOnDataErrors=True,
    ValidatesOnExceptions=True)
    Width="200" Height="25" />

<TextBox x:Name="txtCar" VerticalAlignment="Top"
    Binding Path=Model, Mode=TwoWay,
    UpdateSource=PropertyChanged,
    ValidatesOnDataErrors=True,
    ValidatesOnExceptions=True)
    Width="200" Height="25" />
```

![](bbox=[0.141, 0.853, 0.238, 0.936])

UpdateSourceTrigger enables when the validation calls take.
In this example, validations occur as the text changes, and is fired off
the underlying object fires the PropertyChanged event.

ValidateOnDataErrors enables the IDataErrorInfo vali-
dation to be called on the property.