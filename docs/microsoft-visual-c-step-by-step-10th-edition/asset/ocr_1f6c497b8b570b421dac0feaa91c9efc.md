# Enable an object to notify a binding of a change in a data value

Implement the INotifyPropertyChanged interface in the class that defines the object and raise the PropertyChanged event each time a property value changes. For example:

Click here to view code image

```
class Customer : INotifyPropertyChanged
{
    ...
    public event PropertyChangedEventHandler PropertyChanged;
    protected virtual void OnPropertyChanged(string propertyName)
    {
        if (PropertyChanged is not null)
        {
            PropertyChanged(this, new PropertyChangedEventArgs(propertyName));
        }
    }
```

# Enable a control that uses data binding to update the value of the property to which it is bound

Configure the data binding as two-way. For example:

Click here to view code image

```
<TextBox ... Text="Binding FirstName, Mode=TwoWay" .../>
```

# Separate the business logic runs when a user selects a Button control from the interface that contains the Button control

Use a ViewModel that provides commands implemented with the ICommand interface and bind the Button control to one of these commands. For example:

Click here to view code image

```
<Button xName="nextCustomer" ... Command="{Binding Path=NextCustomer}"/>
```