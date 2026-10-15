```
```csharp
{
    throw new Exception(
        "serialNumber1 does NOT " +
        "reference equal serialNumber2");
}
// And, therefore, they are equal.
else if(!serialNumber1.Equals(serialNumber2))
{
    throw new Exception(
        "serialNumber1 does NOT equal serialNumber2");
}
else
{
    Console.WriteLine(
        "serialNumber1 reference equals serialNumber2");
    Console.WriteLine(
        "serialNumber1 equals serialNumber2");
}

// These serial numbers are NOT the same object identity.
if (ProductSerialNumber.ReferenceEquals(serialNumber1,
        serialNumber3))
{
    throw new Exception(
        "serialNumber1 DOES reference " +
        "equal serialNumber3");
}
// But they are equal (assuming Equals is overloaded).
else if(!serialNumber1.Equals(serialNumber3) ||
        serialNumber1 != serialNumber3)
{
    throw new Exception(
        "serialNumber1 does NOT equal serialNumber3");
}

Console.WriteLine("serialNumber1 equals serialNumber3");
}
```
```

The results of Listing 9.3 appear in Output 9.2.

# OUTPUT 9.2

```
```text
serialNumber1 reference equals serialNumber2
serialNumber1 equals serialNumber3
```
```