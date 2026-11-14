```
return left.CompareTo(right) >= 0;
}
```

```
private static RevenueComparer revComp = null;

// return an object that implements IComparer
// use lazy evaluation to create just one.
public static IComparer<Customer> RevenueCompare
{
    get
    {
        if (revComp == null)
            revComp = new RevenueComparer();
        return revComp;
    }
}
```

```
public static Comparison<Customer> CompareByReview
{
    get
    {
        return (left,right) =>
            left.revenue.CompareTo(right.revenue);
    }
}
```

```
// Class to compare customers by revenue.
// This is always used via the interface pointer,
// so only provide the interface override.
private class RevenueComparer : IComparer<Customer>
{
    #region IComparer<Customer> Members
    int IComparer<Customer>.Compare(Customer left,
        Customer right)
    {
        return left.revenue.CompareTo(
            right.revenue);
    }
    #endregion
}
```