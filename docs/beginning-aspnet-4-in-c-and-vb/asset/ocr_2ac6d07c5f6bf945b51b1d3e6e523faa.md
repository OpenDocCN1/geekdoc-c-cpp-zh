> Another option for a custom error message is to register to the Error event of the Validation class. Here the property NotifyOnValidationError must be set to true.

The error information itself can be accessed from the Errors collection of the Validation class. To display the error information in the ToolTip of the TextBox you can create a property trigger as shown. The trigger is activated as soon as the HasError property of the Validation class is set to True. The trigger sets the ToolTip property of the TextBox:

```
<Style TargetType="{x:Type TextBox}">
    <Style.Triggers>
        <Trigger Property="Validation.HasError" Value="True">
            <Setter Property="ToolTip"
                Value="{Binding RelativeSource=Self,
                    Path=(Validation.Errors)[0].ErrorContent}" />
        </Trigger>
    </Style.Triggers>
</Style>
```

# Data Error Information

Another way to deal with errors is if the .NET object implements the interface IDataErrorInfo.

The class SomeData is now changed to implement the interface IDataErrorInfo. This interface defines the property Error and an indexer with a string argument. With WPF validation during data binding, the indexer is called and the name of the property to validate is passed as the columnName argument. With the implementation the value is verified if it is valid, and an error string is passed otherwise. Here the validation is done on the property Value2 that is implemented by using the C# 3.0 simple property notation:

```
public class SomeData : IDataErrorInfo
{
    //...

    public int Value2 { get; set; }

    string IDataErrorInfo.Error
    {
        get
        {
            return null;
        }
    }

    string IDataErrorInfo.this[string columnName]
    {
        get
        {
            if (columnName == "Value2")
            {
                if (this.Value2 < 0 || this.Value2 > 80)
                    return "age must not be less than 0 or greater than 80";
            }
            return null;
        }
    }
}
```