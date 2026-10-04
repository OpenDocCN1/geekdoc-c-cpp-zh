
# 608 Editing, Validating, Converting, and Visualizing Your Data

4. In the constructor for MainWindow(), ensure that you call the GenerateData() method immediately following the InitializeComponents() call.

5. Run this application.

You see that the values from the DataContext display properly in the TextBox controls. Feel free to change the values in the TextBox controls. For instance, change the value to Athlon X, and the model to ABC. When you finish with your edits, click the Show Current DataContext Value button. The changes you made to the values in the TextBoxes are now reflected in the underlying DataContext object. (See Figure 3-2.)

![](img/6df7bb88e9302e98442acc219cfbd7fc_633_0.png)

Figure 3-2: Editing data using a TwoWay binding.

6. Click the OK button to get rid of the message box.

If you look in the Click event handler of the Change DataContext Value With Code-Behind (btnChangedDataContextValue_Click), you will note that the DataContext Car object will be changed to ChangedMake and Changed Model, respectively.

7. Click the Change DataContext Value With Code-Behind button.

Hmm. Nothing is happening. What is up with that? If you click the Show Current DataContext Value button, you see the properties have been fact changed. Because you're using a TwoWay binding, your settings should automatically update your UI, right? Wrong! This is where another feature of WPF, the concept of INotifyPropertyChanged, comes into play.

INotifyPropertyChanged is a simple interface that allows your objects to raise an event that notifies its subscribers (namely your application) that a property value of the object has changed. Client applications subscribe to these events and update the user interface with the new values when changes occur.

![](img/6df7bb88e9302e98442acc219cfbd7fc_633_1.png)

# Editing, Validating, Converting, and Visualizing Your Data 609

A similar interface exists for collections as well — the INotifyChanged interface. WPF provides a generic class called ObservableCollection<T> that already implements INotifyChanged for you. When creating an Observable Collection or your own collection implements INotifyChanged, you need to ensure that the objects that will be contained within the collection also implement INotifyChanged interface.

Book V
Chapter 3

Data Binding
In WPF

The INotifyPropertyChanged interface contains a single event that must be implemented. This event is called PropertyChanged, and its parameters are the object that has the property that has changed (the sender), and the string name of the property that has changed.

- 8. **Open your Car class and implement the INotifyPropertyChanged interface.**

The interface is located in the System.ComponentModel namespace (using System.ComponentModel to the top of your class) Implementing this interface adds the following event to the Car class:

```
public event PropertyChangedEventHandler PropertyChanged;
```

In order for it to be notified of the changes that occur in Car objects, the PropertyChanged event must be fired each time a property value changes.

- 9. **To implement this in the Car class, create a helper method called NotifyPropertyChanged that takes a string property name and fires the PropertyChanged event for the object instance and the name of the property that has changed, like this:**

```c
private void NotifyPropertyChanged(string propertyName)
{
    if (propertyName != null)
    {
        this.PropertyChanged(this, new PropertyChangedEventArgs(propertyName));
    }
}
```

Checking if PropertyChanged is not essentially means you're checking to whether anyone is listening (subscribed) to the PropertyChanged event.

- 10. **Modify the Set methods in each of the public properties on the Car object to call the NotifyPropertyChanged helper method each time the property value has changed; edit the public properties like this:**

```csharp
public string Make
{
    get { return _make; }
    set
    {
        if (_make != value)
        {
            _make = value;
            NotifyPropertyChanged("Make");
        }
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

# 11. Run the application again.

Now when you click the Change Data Context Value with Code-Behind button, the changed values get reflected automatically in the TextBox elements. This is due to the combination of the TwoWay binding mode as well as the implementation of INotifyPropertyChanged. (See Figure 3-3.)

![](img/6df7bb88e9302e98442acc219cfbd7fc_635_0.png)

Figure 3-3: TwoWay Data Binding with INotify-Property-Changed.

## Validating data

It's good practice to validate any input provided to you from the user. People aren't perfect, and some people can be downright malicious. WPF provides a built-in framework for data validation and error notification. It's available to you through the implementation of the IDataErrorInfo interface on your classes.

You can add validation to the Car class you already created in Binding Sample2 from the preceding section.

## Element binding

In this chapter, you bind Element controls to properties. You're not limited to this scenario; you can bind to anything. For instance, suppose you'd like to have the Label automatically update with the changes. The XAML code looks similar to:

```xml
<Label xName="lblCar" Content="{Binding Text, ElementName=txtCar}" />
```

The C# code looks like:

```csharp
Binding b = new Binding("Text", ElementName="txtCar");
```

The complete solution is available in the Validation2 project. Just these steps to add validation to your Car:

1. Open the Car.cs file and edit the class to also implement IDataErrorInfo interface, like this:

```csharp
public class Car : INotifyPropertyChanged, IDataErrorInfo
{
    public event PropertyChangedEventHandler PropertyChanged;

    public string Error
    {
        get { throw NotImplementedException(); }
    }
}
```

2. Get the Error property to return null.

Now it's time to add some validation rules to the properties of the object. The Car Make and Model properties should be at least three characters in length.

- 3. To define and enforce these rules, edit the public string this[columnName] method like this:

```csharp
public string this[string columnName]
{
    get
    {
        string returnValue = null;
        if (columnName == "Make")
        {
            if (string.IsNullOrEmpty(_make) || _make.Length < 3)
            {
                returnValue = "Car Make must be at least 3 characters in length";
            }
        }
        if (columnName == "Model")
        {
            if (string.IsNullOrEmpty(_model) || _model.Length < 3)
            {
                returnValue = "Car Model must be at least 3 characters in length";
            }
        }
        return returnValue;
    }
}
```

In MainWindow.xaml, the Make and Model properties are bound to TextControls in the user interface.

- 4. To enable the text being entered into the TextBoxes to be validated against the constraints on the underlying property, edit the binding expressions in each TextBox like this:

```xml
<TextBox xName="txtMake" VerticalAlignment="Top"
    Binding Path=Make, Mode=TwoWay,
    UpdateSource=PropertyChanged,
    ValidatesOnDataErrors=True,
    ValidatesOnExceptions=True)
    Width="200" Height="25" />

<TextBox xName="txtModel" VerticalAlignment="Top"
    Binding Path=Model, Mode=TwoWay,
    UpdateSource=PropertyChanged,
    ValidatesOnDataErrors=True,
    ValidatesOnExceptions=True)
    Width="200" Height="25" />
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_637_0.png)

UpdateSourceTrigger enables when the validation calls take. In this example, validations occur as the text changes, and is fired off the underlying object fires the PropertyChanged event.

ValidatesOnDataErrors enables the IDataErrorInfo validation to be called on the property.
