# CHAPTER 9 Using Classes and Objects

To use object initializers, a class must have a default constructor. That is, you either must not create constructors or you must create one that requires no parameters.

Multiple assignments can be made with an object initializer by separating them with commas, as in the following:

```
Employee myAssistant = new Employee {IdNumber = 202, Salary = 25.00};
```

This single line has the same results as the following three statements:

```
Employee myAssistant = new Employee();
myAssistant.IdNumber = 202;
myAssistant.Salary = 25.00;
```

Using object initializers allows you to create multiple objects with different initial assignments without having to provide multiple constructors to cover every situation. Additionally, using object initializers allows you to create objects with different starting values for different properties of the same data type. For example, consider a class like the Box class in Figure 9-32 that contains multiple properties of the same type. The constructor sets the Height, Width, and Depth properties to 1. You could create a constructor that accepts a single integer parameter to be assigned to Height (using the default value 1 for the other dimensions), but then you could not write an additional overloaded constructor that accepts a single integer parameter to be assigned to Width because the constructors would be ambiguous. However, by using initializers, you can create objects to which you assign the properties you want. Figure 9-33 shows a program that declares three Box objects, each with a different assigned dimension, and Figure 9-34 shows the output, which demonstrates that each property was assigned appropriately.

```
class Box
{
    public int Height {get; set;}
    public int Width {get; set;}
    public int Depth {get; set;}
    public Box()
    {
        Height = 1;
        Width = 1;
        Depth = 1;
    }
}
```

**Figure 9-32** The Box class