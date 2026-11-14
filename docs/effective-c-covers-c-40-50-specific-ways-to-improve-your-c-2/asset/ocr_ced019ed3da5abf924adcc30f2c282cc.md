```
```csharp
public Customer(string name)
{
    this.name = name;
}
```
```

```
```csharp
#region IComparable<Customer> Members
public int CompareTo(Customer other)
{
    return name.CompareTo(other.name);
}
#endregion
```
```

```
```csharp
#region IComparable Members
int IComparable.CompareTo(object obj)
{
    if (!(obj is Customer))
        throw new ArgumentException(
            "Argument is not a Customer", "obj");
    Customer otherCustomer = (Customer)obj;
    return this.CompareTo(otherCustomer);
}
#endregion
```
```

```
```csharp
// Relational Operators.
public static bool operator <(Customer left,
    Customer right)
{
    return left.CompareTo(right) < 0;
}
public static bool operator <=(Customer left,
    Customer right)
{
    return left.CompareTo(right) <= 0;
}
public static bool operator >(Customer left,
    Customer right)
{
    return left.CompareTo(right) > 0;
}
```
```