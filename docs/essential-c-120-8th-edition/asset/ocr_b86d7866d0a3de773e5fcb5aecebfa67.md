# 412 Chapter 7: Inheritance

```
public virtual string Name { get; set; }
public abstract string GetSummary();
}
```

```
public class Contact : PdaItem
{
    //...
    public override string Name
    {
        get
        {
            return $"{FirstName} {LastName}";
        }
        set
        {
            string[] names = value.Split(' ');
            // Error handling not shown
            FirstName = names[0];
            LastName = names[1];
        }
    }
}
```

```
public string FirstName
{
    get
    {
        return _FirstName!;
    }
    set
    {
        _FirstName = value ??
            throw new ArgumentNullException(nameof(value)); ;
    }
}
```

```
private string? _FirstName;
public string LastName
{
    get
    {
        return _LastName!;
    }
    set
    {
        _LastName = value ?? throw new ArgumentNullException(nameof(value));
    }
}
```