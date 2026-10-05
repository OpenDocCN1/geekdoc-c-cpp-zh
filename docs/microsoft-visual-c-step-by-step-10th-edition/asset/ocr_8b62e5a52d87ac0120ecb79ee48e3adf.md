```
public class Customer : INotifyPropertyChanged
{
    private string _phone;
    public string Phone
    {
        get => this._phone;
        set { this._phone = value; }
    }
    public event PropertyChangedEventHandler PropertyChanged;
}
```

This is the event item that the INotifyPropertyChanged interface defines. All objects that implement this interface must provide this event, and they will raise this event whenever they want to notify the outside world of a change to a property value.

+   5. Add the OnPropertyChanged method shown here in bold to the Customer class, after the PropertyChanged event:

```
class Customer : INotifyPropertyChanged
{
    public event PropertyChangedEventHandler PropertyChanged;
    protected virtual void OnPropertyChanged(string propertyName)
    {
        if (PropertyChanged is not null)
        {
            PropertyChanged(this, new PropertyChangedEventArgs(propertyName));
        }
    }
}
```

The OnPropertyChanged method raises the PropertyChanged event. The PropertyChangedEventArgs parameter to the PropertyChanged event should specify the name of the property that has changed. This value is passed in as a parameter to the OnPropertyChanged method.