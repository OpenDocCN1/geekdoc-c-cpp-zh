# BEGINNER TOPIC

# Objects and Classes Defined

In casual conversation, the terms class and object appear interchangeably. However, they actually have distinct meanings. A class is a template for an object will look like at instantiation time. An object, therefore, is an instance of a class. Classes are the mold for what a widget will look like; objects correspond to widgets created by the mold. The process of creating an object from a class is called instantiation because an object is an instance of a class.

Now that you have defined a new class type, it is time to instantiate an object of that type. Mimicking its predecessors, C# uses the new keyword to instantiate an object (see Listing 6.3).

Listing 6.3: Instantiating a Class

```
public class Program
{
    public static void Main()
    {
        Employee employee1 = new Employee();
        Employee employee2;
        Employee employee2 = new Employee();

        IncreaseSalary(employee1);
        IncreaseSalary(employee2);
    }
    // ...n
```

Not surprisingly, the assignment can occur either in the same statement as the declaration or in a separate statement.

Unlike the primitive types you have worked with so far, there is no literal way to specify an Employee. Instead, the new operator provides an instruction to the