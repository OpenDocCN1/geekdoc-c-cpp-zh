# The IDisplayable interface

```
interface IDisplayable
{
    string GetDisplayText(string sep);
}
```

# A Product class that implements the IDisplayable interface

```
public class Product : IDisplayable
{
    public string Code { get; set; }
    public string Description { get; set; }
    public decimal Price { get; set; }

    public Product(string Code, string Description, decimal Price)
    {
        this.Code = Code;
        this.Description = Description;
        this.Price = Price;
    }

    public string GetDisplayText(string sep) =>
        this.Code + sep + this.Description + sep + this.Price.ToString("c");
}
```

# Code that uses the IDisplayable interface

```
IDisplayable product = new Product("C#", "Murach's C#", 59.50m);
Debug.WriteLine(product.GetDisplayText("\n"));
```

# A comparison of interfaces and abstract classes

+   - Both interfaces and abstract classes can provide signatures for properties and methods that a class must implement.
+   - Both interfaces and abstract classes can implement some or all of their properties and methods.
+   - An abstract class can use instance variables and constants as well as static variables and constants. An interface can only use static variables and constants.
+   - A class can inherit only one class (including abstract classes), but a class can implement more than one interface.

# Description

+   - An *interface* consists of a set of signatures for one or more methods, properties, indexers, or events.
+   - With C# 8.0 and later, an interface can provide implementation for its *default interface members*. Default interface members may be overridden by any class that *implements* the interface, and all non-default interface members must be defined by those classes. By convention, interface names begin with the letter I to distinguish them from classes.
+   - To implement an interface, a class must name the interface on the class declaration, and it must provide an implementation for every non-default member of the interface.