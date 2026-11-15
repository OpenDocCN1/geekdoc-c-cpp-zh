```
}
public override bool Equals(object obj)
{
    if (obj == null)
    {
        return false;
    }

    if (ReferenceEquals(this, obj))
    {
        return true;
    }

    if (this.GetType() != obj.GetType())
    {
        return false;
    }

    return Equals((ProductSerialNumber)obj);
}
```

```
public bool Equals(ProductSerialNumber obj)
{
    // STEP 3: Possibly check for equivalent hash codes
    // if (this.GetHashCode() != obj.GetHashCode())
    // {
    //     return false;
    // }
    //
    //

    // STEP 4: Check base.Equals if base overrides Equals()
    // System.Diagnostics.Debug.Assert(
    //     base.GetType() == typeof(object);
    //     if ( base.Equals(obj) )
    //     {
    //         return false;
    //     }
    // }

    // STEP 1: Check for null
    return (obj != null)
        // STEP 5: Compare identifying fields for equality.
        && (ProductSeries == obj.ProductSeries) &&
        (Model == obj.Model) &&
        (Id == obj.Id));
}
```

```
public static bool operator ==(
    ProductSerialNumber leftHandSide,
    ProductSerialNumber rightHandSide)
{
    // Check if leftHandSide is null.
    // (operator== would be recursive)
}
```