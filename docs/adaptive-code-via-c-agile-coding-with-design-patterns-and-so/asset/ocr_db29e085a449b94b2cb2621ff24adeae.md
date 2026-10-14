```
```csharp
: base(flatRate)
{
}

public new decimal FlatRate
{
    get
    {
        return base.FlatRate;
    }
    set
    {
        base.FlatRate = value;
    }
}
}
// . . .
public class ShippingStrategy
{
    public ShippingStrategy(decimal flatRate)
    {
        if (flatRate <= decimal.Zero)
            throw new ArgumentOutOfRangeException("flatRate", "Flat rate must be positive and non-zero");

        this.flatRate = flatRate;
    }

    protected decimal FlatRate
    {
        get
        {
            return flatRate;
        }
        set
        {
            if (value <= decimal.Zero)
                throw new ArgumentOutOfRangeException("value", "Flat rate must be positive and non-zero");

            flatRate = value;
        }
    }
}
```
```