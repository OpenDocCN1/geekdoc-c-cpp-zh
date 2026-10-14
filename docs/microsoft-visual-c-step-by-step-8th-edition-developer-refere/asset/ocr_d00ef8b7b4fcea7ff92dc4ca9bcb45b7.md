```
protected virtual void OnPropertyChanged(string propertyName)
{
    if (PropertyChanged != null)
    {
        PropertyChanged(this,
            new PropertyChangedEventArgs(propertyName));
    }
}
```

The *OnPropertyChanged* method raises the *PropertyChanged* event. The *PropertyChangedEventArgs* parameter to the *PropertyChanged* event should specify the name of the property that has changed. This value is passed in as a parameter to the *OnPropertyChanged* method.

6. Modify the property set accessors for each of the properties in the *Customer* class to call the *OnPropertyChanged* method whenever the value that they contain is modified, as shown in bold here:

Click here to view code image

```
class Customer : INotifyPropertyChanged
{
    public int _customerID;
    public int CustomerID
    {
        get { return this._customerID; }
        set
        {
            this._customerID = value;
            this.OnPropertyChanged(nameof(CustomerID));
        }
    }
    public string _title;
    public string Title
    {
        get { return this._title; }
        set
        {
            this._title = value;
            this.OnPropertyChanged(nameof(Title));
        }
    }
    public string _firstName;
    public string FirstName
    {
        get { return this._firstName; }
        set
        {
            this._firstName = value;
            this.OnPropertyChanged(nameof(FirstName));
        }
    }
}
```