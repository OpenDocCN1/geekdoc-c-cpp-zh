
## Two Product objects that have been instantiated from the Product class

| product1 |
|----------|
| Code=C# |
| Description=Murach's C# |
| Price=59.50 |

| product2 |
|----------|
| Code=ASPMVC |
| Description=Murach's ASP.NET MVC |
| Price=61.50 |

## Code that declares and creates these two object instances

```
Product product1, product2;
product1 = new Product("C#", "Murach's C#", 59.50m);
product2 = new Product("ASPMVC", "Murach's ASP.NET MVC", 61.50m);
```

## Code that creates an object and initializes it manually

```
product1 = new Product();
product1.Code = "C#";
product1.Description = "Murach's C#";
product1.Price = 59.50m;
```

## Code that creates an object with an object initializer

```
product1 = new Product {
    Code = "C#",
    Description = "Murach's C#",
    Price = 59.50m
};
```

## Three ways to declare and create an object in a single statement

```
Product product3 = new Product();      // explicitly typed
var product4 = new Product();          // implicitly typed
Product product5 = new();              // with C# 9.0 and later
```

## Description

- When an object is instantiated, a *constructor* is executed to initialize the data that makes up the object. If a class doesn’t provide a constructor, a default constructor is executed. The default constructor simply initializes all the data to default values.
- The data that makes up an object is sometimes referred to as the object’s *state*. Once an object has been instantiated, its state can change.
- The state of an object changes whenever you change the value of one of the object’s properties or public fields. The state can also change when you call a method that affects the data stored within an object.
- An application can create two or more instances of the same class. Each instance is a separate entity with its own state. If you change the state of one object, the state of other objects created from the same class is not affected.
- *Object initializers* let you create an instance of an object and assign values to that object in a single statement without explicitly calling a constructor.
- A class defines a *reference type*. That means that the variable that’s used to access an object instantiated from a class contains the address of the object, not the actual object.

## Basic skills for creating a class

Now that you’ve learned about the members that make up a class and you’ve seen the code for the Product class, you’re ready to learn the basic skills for creating and using your own classes. The topics that follow present these skills.

## How to add a class file to a project

To create a user-defined class, you start by adding a *class file* to your project. To do that, you use the dialog box shown in figure 12-5. When you complete this dialog box, the class file will appear in the Solution Explorer with the extension *cs*.

When you add a class to a project, Visual Studio automatically generates the class declaration. Then, you can complete the class by adding fields, constructors, properties, methods, and whatever other members the class may require.

## The dialog box for adding a class

![](img/844f608d10a44654833ea5efc8a2e7a7_406_0.png)

## The starting code for the new class

```
using System;
using System.Collections.Generic;
using System.Text;

namespace ProductMaintenance
{
    class Product
    {
    }
}
```

## Description

- To add a new class to a project, use the Project→Add Class Item command to display the Add New Item dialog box. Then, enter the name you want to use for the new class and click the Add button.
- When you complete the Add New Item dialog box, a class file is added to the project. This class file will appear in the Solution Explorer window with the extension cs.
- The namespace and class blocks are automatically added to the class. Then, you can enter the code for the class within the class block.

## How to code fields

Figure 12-6 shows how to code the fields that define the variables used by a class. A class can contain two types of fields: *instance variables* and *static variables*. This figure shows you how to work with instance variables. You’ll learn about static variables in figure 12-10.

When you declare a field, you should use an access modifier to control the accessibility of the field. If you specify *private* as the access modifier, the field can be used only within the class that defines it. By contrast, if you specify *public* as the access modifier, the field can be accessed by other classes. You can also use other access modifiers that give you finer control over the accessibility of your fields. You’ll learn about those modifiers in chapter 14.

This figure shows three examples of field declarations. The first example declares a private field of type int. The second declares a public field of type decimal.

The third example declares a *read-only field*. As its name implies, a read-only field can be read but not modified. In this respect, a read-only field is similar to a constant. The difference is that the value of a constant is set when the class is compiled, while the value of a read-only field is set at runtime. You can assign a value to a read-only field when you declare it as shown in the third example or in the code for one of the constructors of the class.

Note that although fields work like regular variables, they must be declared within the class body, not inside properties, methods, or constructors. That way, they’re available throughout the entire class. In this book, all of the fields for a class are declared at the beginning of the class. However, when you read through code from other sources, you may find that the fields are declared at the end of the class or at other locations within the class.

This figure also presents another version of the Product class that uses public fields instead of properties. This works because the properties of the Product class that was presented in figure 12-3 didn’t do anything except get and set the values of private fields. Because of that, you could just provide direct access to the fields by giving them public access as shown here. In some cases, though, a property will perform additional processing. Then, you’ll need to use a property instead of a public field.

By the way, you may notice that the names of the public fields in this class and in the second and third examples at the beginning of this figure begin with a capital letter. That’s because these fields are used in place of properties, and the names of properties are always capitalized. By contrast, the name of the private field in the first example begins with a lowercase letter because it can only be accessed within the class.

## Examples of field declarations

```
private int quantity;        // A private field
public decimal Price;        // A public field
public readonly int Limit = 90;  // A public read-only field
```

## A version of the Product class that uses public fields instead of properties

```
public class Product
{
    // Public fields
    public string Code;
    public string Description;
    public decimal Price;

    public Product()
    {
    }

    public Product(string code, string description, decimal price)
    {
        this.Code = code;
        this.Description = description;
        this.Price = price;
    }

    public string GetDisplayText(string sep)
    {
        return Code + sep + Price.ToString("c") + sep + Description;
    }
}
```

## Description

- A variable that’s defined at the class level within a class is called a field.
- A field can be a primitive data type, a .NET class or structure, or a user-defined class or structure.
- You can use the private access modifier to prevent other classes from accessing a field. Then, the field can be accessed only from within the class.
- An instance variable is a field that’s defined in a class and is allocated when an object is instantiated. Each object instance has a separate copy of each instance variable.
- If you initialize an instance variable when you declare it, the initialization will occur before the constructor for the class is executed. As a result, the constructor may assign a new value to the variable.
- You can create a read-only field by specifying the readonly keyword in the field’s declaration. Then, the field’s value can be retrieved, but it can’t be changed. You can set the value for a read-only field when you declare it or in the code for a constructor.
- A public field is a field that’s declared with the public access modifier. Public fields can be accessed by other classes within the application, much like properties. However, properties can have additional features that make them more useful than public fields.
