# IDisplayable interface

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

    public string GetDisplayText(string sep)
    {
        return this.Code + sep + this.Price.ToString("c");
    }
}
```

# Code that uses the IDisplayable interface

```
IDisplayable product = new Product("CS10", "Murach's C# 2010", 54.5m);
Console.WriteLine(product.GetDisplayText("\n"));
```

# A comparison of interfaces and abstract classes

+   * Interfaces and abstract classes provide signatures for properties and methods that a class must implement.
* All of the members of an interface are abstract. In contrast, an abstract class can implement some or all of its members.
* A class can inherit only one class (including abstract classes), but a class can implement more than one interface.
* Interfaces can't declare static members, but abstract classes.

# Description

+   * An interface consists of a set of signatures for one or more methods, properties, indexes, or events. An interface doesn't provide an implementation for any of its members. Instead, it indicates what members must be defined by any class that implements the interface.
* By convention, interface names begin with the letter I to distinguish them from classes.
* To implement an interface, a class must name the interface on the class declaration, and it must provide an implementation for every member of the interface.

![](bbox=[0.062, 0.953, 0.435, 0.967])