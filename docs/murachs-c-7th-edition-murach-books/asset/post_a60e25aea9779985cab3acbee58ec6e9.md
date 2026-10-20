
## The code for the cloneable Product class

```
public class Product : IDisplayable, ICloneable
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

	public object Clone()
	{
		Product p = new Product();
		p.Code = this.Code;
		p.Description = this.Description;
		p.Price = this.Price;
		return p;
	}
}
```

## Code that creates and clones a Product object

```
Product p1 = new Product("BJWN", "Murach's Beginning Java with NetBeans",
57.50m);
Product p2 = (Product)p1.Clone();
p2.Code = "BJWE";
p2.Description = "Murach's Beginning Java with Eclipse";
Debug.WriteLine(p1.GetDisplayText("\n") + "\n");
Debug.WriteLine(p2.GetDisplayText("\n") + "\n");
```

## The output that's displayed by the code shown above

```
BJWN
Murach's Beginning Java with NetBeans
$57.50

BJWE
Murach's Beginning Java with Eclipse
$57.50
```

## How to use an interface as a parameter

Figure 15-6 shows how to use an interface as a parameter of a method. To do that, you code the name of the interface as the parameter type as shown in the first example. Here, a method named CreateList() accepts two parameters: an object that implements ICloneable and an integer. This method returns a list that’s filled with copies of the object specified by the first parameter. The number of copies to be included in the list is specified by the second parameter. To generate the copies, the CreateList() method uses the Clone() method of the object that’s passed to it.

The second example shows how to code a method named WriteToDebug() that accepts the IDisplayable interface as a parameter. This method uses the GetDisplayText() method of the IDisplayable interface to return the display text for the object. Then, it uses the WriteLine() method of the Debug class to write this text to the Output window.

When you declare a method that accepts an interface as a parameter, you can pass any object that implements that interface to the method. This is illustrated by the third code example in this figure. Here, a new Product object is created and stored in a variable named product. Then, the CreateList() method is used to create three copies of the Product object. And finally, the WriteToDebug() method is used to write each Product object to the Output window. You can see the result in the last example in this figure.

The key point here is that the CreateList() method doesn’t know what type of object it’s cloning. All it knows is that the object implements the ICloneable interface, which means that it has a Clone() method. Similarly, the WriteToDebug() method doesn’t know what type of object it’s writing to the Output window. All it knows is that the object implements the IDisplayable interface. Both of these methods work for the Product object because the Product class implements ICloneable and IDisplayable.

This example illustrates an even larger point. In short, a Product object can be thought of as an ICloneable or IDisplayable object. As a result, you can supply a Product object anywhere an ICloneable or IDisplayable object is expected. In this figure, interfaces are used to specify the type for a parameter of a method. However, interfaces can be used to specify a type in other places too. For example, an interface can be used as a return type for a method. Similarly, an interface can be used to specify the type of a property. And anywhere an interface is used to specify a type, you can supply any object that implements that interface.

## A CreateList() method that uses an interface as a parameter

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

## A WriteToDebug() method that uses an interface as a parameter

```
public static void WriteToDebug(IDisplayable d) =>
    Debug.WriteLine(d.GetDisplayText("\n") + "\n");
```

## Code that uses these methods

```
Product product = new Product("C#", "Murach's C#", 59.50m);
List<object> products = CreateList(product, 3);
foreach (Product p in products)
{
    WriteToDebug(p);
}
```

## The output that's displayed by the code shown above

```
C#
Murach's C#
$59.50

C#
Murach's C#
$59.50

C#
Murach's C#
$59.50
```

## Description

- You can declare a parameter that’s used by a method as an interface type. Then, you can pass any object that implements the interface to the parameter.
- Since the Product class implements both the ICloneable and IDisplayable interfaces, it can be passed as an argument to a method that accepts an object of the ICloneable or IDisplayable type.

## How to work with default methods

Prior to C# 8.0, interfaces could only contain abstract methods and any class that implemented an interface had to implement all the methods of that interface. This was a significant problem because if you changed an interface by adding or modifying a method, you also had to update any class that implemented the interface so it implemented the new or modified method.

Fortunately, C# 8.0 provides a new feature that allows you to include regular (non-abstract) methods in interfaces, known as default methods. Now, if a class implements an interface, it doesn’t have to override the default methods of the interface. Instead, it can use these default methods. However, whenever necessary, a class can override a default method to change its functionality.

The first example in figure 15-7 shows an interface declares a default method named GetDisplayText() that accepts a string parameter named terminator. This method calls the ToString() method from the object that implements the interface to get a String object that represents the object. Then it returns that String object with the terminator appended to it.

Next, this example shows a class that implements this interface and uses the default GetDisplayText() method. Since this method is included in the interface, this class doesn’t need to implement the GetDisplayText() method. Instead, it can use the functionality that’s provided by the default method in the interface. This works as if the class has inherited the method from another class.

Finally, this example shows a class that implements the interface in the first example and overrides the GetDisplayText() method. This allows the class to change the functionality that’s provided by the default method. Note that you can’t use the override keyword when overriding a default method of an interface. If you do that, you’ll get a compiler error.

## How to work with static methods and fields

With C# 8.0 and later, you can also code static methods and fields in interfaces, as shown in the second example in figure 15-7. Here, an interface named IPrintable contains a static field named terminator and a static method named Print() that accepts a parameter of the IDisplayable type. This method contains a single line of code that calls the GetDisplayText() method of the IDisplayable object.

Next, this example shows code that uses the IPrintable interface. To start, the first statement creates an IDisplayable object named product. Then, the second statement passes this object to the static Print() method of the IPrintable interface. As you can see, this works much like calling a static method from a class.

## The syntax for declaring a default method (C# 8.0 or later)

```
accessModifier returnType MethodName({[parameterlist]}) { ... }
```

## An interface that defines a default method

```
public interface IDisplayable {
string GetDisplayText(string terminator) {
return ToString() + terminator;
}
...
}
```

## A class that uses the default method

```
public class Product : IDisplayable {
// This class doesn't override the GetDisplayText() method.
// As a result, it uses the GetDisplayText() method defined
// by the interface.
}
```

## A class that overrides the default method

```
public class Product : IDisplayable {
public string GetDisplayText(string sep) {
return this.Code + sep + this.Description + sep + this.Price;
}
}
```

## An interface that defines a static method and a static field

```
public interface IPrintable {
static string terminator = "\r\n";
static string Print(IDisplayable p) {
return p.GetDisplayText(terminator);
}
}
```

## Code that calls a static method from an interface

```
IDisplayable product = new Product("C#", "Murach's C#", 59.50m);
IPrintable.Print(product);
```

## Description

- With C# 8.0 and later, you can add regular (non-abstract) methods to an interface. These methods are known as default methods, and they have the same syntax as a method in a class.
- When you code a class that implements an interface, you don’t need to implement its default methods. Instead, you can use the default methods defined in the interface in your class. However, if you want to change the functionality of a default method, you can override it.
- With C# 8.0 or later, you can include static methods and fields in interfaces. To call a static method or to refer to a static field in an interface, prefix the method or field with the name of the interface.
