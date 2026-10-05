```
class Customer : INotifyPropertyChanged
{
    ...
    public event PropertyChangedEventHandler
        PropertyChanged;
    protected virtual void OnPropertyChanged(
        string propertyName)
    {
        if (PropertyChanged is not null)
        {
            PropertyChanged(this,
                new PropertyChangedEventArgs(propertyName));
        }
    }
}
```