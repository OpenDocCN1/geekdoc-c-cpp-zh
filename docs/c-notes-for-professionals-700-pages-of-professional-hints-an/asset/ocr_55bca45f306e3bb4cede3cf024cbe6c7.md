# Chapter 88: INotifyPropertyChanged interface

# Section 88.1: Implementing INotifyPropertyChanged in C# 6

The implementation of INotifyPropertyChange can be error-prone, as the interface requires specifying property name as a string. In order to make the implementation more robust, an attribute CallerMemberName can be used.

```
```csharp
class C : INotifyPropertyChanged
{
    // backing field
    int offset;
    // property
    public int Offset
    {
        get
        {
            return offset;
        }
        set
        {
            if (offset == value)
                return;
            offset = value;
            RaisePropertyChanged();
        }
    }

    // helper method for raising PropertyChanged event
    void RaisePropertyChanged([CallerMemberName] string propertyName = null) =>
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));

    // interface implementation
    public event PropertyChangedEventHandler PropertyChanged;
}
```
```

If you have several classes implementing INotifyPropertyChanged, you may find it useful to refactor out the interface implementation and the helper method to the common base class:

```
```csharp
class NotifyPropertyChangedImpl : INotifyPropertyChanged
{
    protected void RaisePropertyChanged([CallerMemberName] string propertyName = null) =>
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));

    // interface implementation
    public event PropertyChangedEventHandler PropertyChanged;
}
```
```

```
```csharp
class C : NotifyPropertyChangedImpl
{
    int offset;
    public int Offset
    {
        get { return offset; }
        set { if (offset != value) { offset = value; RaisePropertyChanged(); } }
    }
}
```
```