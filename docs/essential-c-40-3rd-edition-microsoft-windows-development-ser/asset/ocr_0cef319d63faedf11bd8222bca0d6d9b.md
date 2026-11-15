```
// Id property declaration
public string Id
{
    get
    {
        return _id;
    }
    // Providing an access modifier is in C# 2.0
    // and higher only
    private set
    {
        _id = value;
    }
}
private string _id;
}
```

By using private on the setter, the property appears as read-only to classes other than Employee. From within Employee, the property appears as read/write, so you can assign the property within the constructor. When specifying an access modifier on the getter or setter, take care that the access modifier is more restrictive than the access modifier on the property as a whole. It is a compile error, for example, to declare the property as private and the setter as public.

# Properties as Virtual Fields

As you have seen, properties behave like virtual fields. In some instances, you do not need a backing field at all. Instead, the property getter returns a calculated value while the setter parses the value and persists it to some other member fields (if it even exists). Consider, for example, the Name property implementation shown in Listing 5.22. Output 5.7 shows the results.

# LISTING 5.22: Defining Properties

```
class Program
{
    static void Main()
    {
        Employee employee1 = new Employee();
        employee1.Name = "Inigo Montoya";
        System.Console.WriteLine(employee1.Name);
    }
}
```