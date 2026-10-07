To define an abstract class, C# requires the abstract modifier to the class definition, as shown in Listing 7.16.

# Listing 7.16: Defining an Abstract Class

```
// Define an abstract class
public abstract class PdaItem
{
    public PdaItem(string name)
    {
        Name = name;
    }
    public virtual string Name { get; set; }
}

public class Program
{
    public static void Main()
    {
        // ERROR: Cannot create an instance of the abstract class
        PdaItem item = new("Inigo Montoya");
    }
}
```

Although abstract classes cannot be instantiated, this restriction is a minor characteristic of an abstract class. Their primary significance is achieved when abstract classes include abstract members. An abstract member is a method or property that has no implementation. Its purpose is to force all derived classes to provide the implementation.

Consider Listing 7.17 as an example.

# Listing 7.17: Defining Abstract Members

```
using static System.Environment;

// Define an abstract class
public abstract class PdaItem
{
    public PdaItem(string name)
    {
        Name = name;
    }
}
```