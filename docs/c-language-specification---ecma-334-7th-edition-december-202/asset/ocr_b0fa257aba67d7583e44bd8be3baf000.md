```
```csharp
public string Name
{
    get => name;
    set
    {
        OnNameChanging(value);
        name = value;
        OnNameChanged();
    }
}

partial void OnNameChanging(string newName);
partial void OnNameChanged();
```
```

If this class is compiled without any other parts, the defining partial method declarations and their invocations will be removed, and the resulting combined class declaration will be equivalent to the following:

```
```csharp
class Customer
{
    string name;

    public string Name
    {
        get => name;
        set => name = value;
    }
}
```
```

Assume that another part is given, however, which provides implementing declarations of the partial methods:

```
```csharp
partial class Customer
{
    partial void OnNameChanging(string newName) =>
        Console.WriteLine($"Changing {name} to {newName}");

    partial void OnNameChanged() =>
        Console.WriteLine($"Changed to {name}");
}
```
```

Then the resulting combined class declaration will be equivalent to the following:

```
```csharp
class Customer
{
    string name;

    public string Name
    {
        get => name;
        set
        {
            OnNameChanging(value);
            name = value;
            OnNameChanged();
        }
    }
}
```
```