# Listing 4-13: The Customer Model Class

```
public class Customer : ModelBase
{
    private string _name;
    private SalesRegion _region;
    public int ID { get; set; }
    public string Name
    {
        get { return _name; }
        set {
            if (value == _name)
            {
                return;
            }
            _name = value;
            NotifyPropertyChanged(this, "Name");
        }
    }
    public SalesRegion SalesRegion
    {
        get { return _region; }
        set {
            if (value == _region)
            {
                return;
            }
            _region = value;
            NotifyPropertyChanged(this, "SalesRegion");
        }
    }
}
```

# Listing 4-14: The SalesRegion Model Class

```
public class SalesRegion:ModelBase
{
    private string _name;
    public int ID { get; set; }
    public string Name
    {
        get { return _name; }
        set {
            if (value == _name)
            {
                return;
            }
            _name = value;
            NotifyPropertyChanged(this, "Name");
        }
    }
}
```