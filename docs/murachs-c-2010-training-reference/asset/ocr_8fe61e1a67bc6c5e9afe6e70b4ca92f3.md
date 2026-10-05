# CreateList method that uses an interface as a parameter

```
public static List<object> CreateList(ICloneable obj, int count)
{
    List<object> objects = new List<object>();
    for (int i = 0; i < count; i++)
    {
        object o = obj.Clone();
        objects.Add(o);
    }
    return objects;
}
```

# WriteToConsole method that uses an interface as a parameter

```
public static void WriteToConsole(IDisplayable d)
{
    Console.WriteLine(d.GetDisplayText("\n") + "\n");
}
```

# Code that uses these methods

```
Product product = new Product("CS10", "Murach's C# 2010", 54.50m);
List<object> products = CreateList(product, 3);
foreach (Product p in products)
{
    WriteToConsole(p);
}
```

# The output displayed by the code shown

```
CS10
Murach's C# 2010
$54.50

CS10
Murach's C# 2010
$54.50

CS10
Murach's C# 2010
$54.50
```

# Description

+   - You can declare a parameter that's used by a method as an interface type. Then, you can pass any object that implements the interface to the parameter.

+   - Since the Product class implements both the ICloneable and IDisplayable interfaces, it can be passed as an argument to a method that accepts an object of the ICloneable or IDisplayable type.