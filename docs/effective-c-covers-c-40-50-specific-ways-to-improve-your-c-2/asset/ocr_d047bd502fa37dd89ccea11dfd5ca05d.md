```
private string URL;
private string description;

#region IComparable<URLInfo> Members
public int CompareTo(URLInfo other)
{
    return URL.CompareTo(other.URL);
}
#endregion

#region IComparable Members
int IComparable.CompareTo(object obj)
{
    if (obj is URLInfo)
    {
        URLInfo other = (URLInfo)obj;
        return CompareTo(other);
    }
    else
    {
        throw new ArgumentException(
            "Compared object is not URLInfo");
    }
}
#endregion
}
```

You can create a sorted list of URLInfo objects easily because URLInfo implements IComparable<T> and IComparable. Even code that relies on the classic IComparable will have fewer times when boxing and unboxing is necessary because the client can call IComparable.CompareTo() without unboxing the object.

Base classes describe and implement common behaviors across related concrete types. Interfaces describe atomic pieces of functionality that unrelated concrete types can implement. Both have their place. Classes define the types you create. Interfaces describe the behavior of those types as pieces of functionality. If you understand the differences, you will create more expressive designs that are more resilient in the face of change. Use class hierarchies to define related types. Expose functionality using interfaces implemented across those types.