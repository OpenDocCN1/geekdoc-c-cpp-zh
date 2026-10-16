```
{
    public int Id
    {
        get; set;
    }
    public string FirstName
    {
        get; set;
    }
    public string LastName
    {
        get; set;
    }
    public string Address
    {
        get; set;
    }
}
```

In the next snippet, you can see how to use reflection to get the name of the class and Customer class namespace name:

```
Type type = typeof(Customer);
Console.WriteLine("Class: " + type.Name);
Console.WriteLine("Namespace: " + type.Namespace);
```

Here you can see how to retrieve a list of the Customer class properties and have their names displayed in the console window:

```
static void Main(string[] args)
```