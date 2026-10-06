
# Creating Objects

In the statement `myAssistant = new Employee();` the last part of the statement after the new operator, `Employee()`, looks suspiciously like a method name with parentheses. It is, in fact, name of a method that constructs an Employee object. `Employee()` is a constructor. You will write your own constructors in this chapter. For now, note that when you do not write a constructor for a class, C# writes one for you, and the name of the constructor is always the same as the name of the class which objects constructs.

Later this chapter you will learn that the automatically-generated constructor for a class is a default constructor, which means it takes parameters. Programmers erroneously equate the terms automatically-generated and default. The automatically created constructor for a class is an example of a default constructor, but you can explicitly create your own default constructor.

After an object has been instantiated, its nonstatic public members can be accessed using the object's identifier, a dot, and the public member's identifier. For example, if you declare an Employee named `myAssistant`, you can access `myAssistant.WelcomeMessage();`.

An object like `myAssistant` that uses an instance method is an invoking object. The statement `myAssistant.WelcomeMessage();` would be illegal if `WelcomeMessage()` was a static method. The method can be used appropriately with each unique Employee object because it is nonstatic.

A program that declares `myAssistant` cannot access its `idNumber` directly; the only way a program can access the private data is by using one of the object's public methods. Because the `WelcomeMessage()` method is part of the class as `idNumber`, and because `WelcomeMessage()` is public, a client method (for example, a `Main()` method in a program) can use the method. Figure 9-4 shows a class `CreateEmployee` whose `Main()` method declares an Employee and displays the Employee's welcome message. Figure 9-5 shows the execution of the program.

```cs
using static System.Console;
class CreateEmployee
{
    static void Main()
    {
        Employee myAssistant = new Employee();
        myAssistant.WelcomeMessage();
    }
}
```

**Figure 9-4** The CreateEmployee program

# CHAPTER 9 Using Classes and Objects

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_386_0.png)

**Figure 9-5** Output of the CreateEmployee program

In the output in 9-5, the Employee's ID number is 0. By default, all unassigned numeric fields in an object are initialized to 0. When you compile the program in Figure 9-4, you receive a warning message:

Field `Employee.idNumber` is never assigned to, and will always have its default value 0.

Of course, usually you want to provide a different value for each Employee's `idNumber` field. One way to provide values for object fields is to create properties, which you will do later in this chapter.

# Passing Objects to Methods

A class represents a data type, and you can pass objects to methods just as you can pass variables that are simple types. For example, the program in Figure 9-6 shows how string variables and Employee objects can be passed to a `DisplayEmployeeData()` method. Each Employee is assigned to the `emp` parameter within the method. Figure 9-7 shows the program's output.

```cs
using System;
class CreateTwoEmployees
{
    static void Main()
    {
        Employee aWorker = new Employee();
        Employee anotherWorker = new Employee();
        DisplayEmployeeData("First", aWorker);
        DisplayEmployeeData("Second", anotherWorker);
    }
    static void DisplayEmployeeData(string order, Employee emp)
    {
        Console.WriteLine("\n" + order + " employee's message: " + emp.WelcomeMessage());
    }
}
```

**Figure 9-6** The CreateTwoEmployees program

```
First employee's message:
Welcome from Employee #0
How can I help you?

Second employee's message:
Welcome from Employee #0
How can I help you?
```

**Figure 9-7** Output of the CreateTwoEmployees program

When you pass an object to a method, any change made to an object parameter in a method also affects the object used as an argument in the calling method.

In 9-6, the `DisplayEmployeeData()` method is internal by default. Because the method accepts an Employee parameter; it must be no more accessible than the Employee class, which is also internal. This restriction preserves the security provided for the Employee class's non members. The program would also work if you made both the `DisplayEmployeeData()` method and the Employee class public.

# TWO TRUTHS & A LIAR

1. Declaring a class creates one object of a new data type.
2. After you declare a class, you must use the new operator to allocate memory for an object of that class and to instantiate it.
3. After an object has been instantiated, its public members can be accessed using the object's identifier, a dot, and a method call.

# Creating Properties

Frequently, methods you call with an object are used to alter the states of its fields. For example, you might want to set the date or time of a party. In the Employee class, you could write a method such as `SetIDNumber()` to set an employee's `idNumber` field as follows:

```cs
public void SetIDNumber(int number)
{
    idNumber = number;
}
```

Then, after you instantiate an Employee object named `myAssistant`, you could call the method like the following:
`myAssistant.SetIdNumber(785);`

Although this technique would work, and might be used in other programming languages, programmers more often create properties to perform similar tasks. A property is member of a class that provides access to a field of class; properties define how fields will be set and retrieved. C# programmers refer to properties as smart fields because they provide a combination of the best features of private fields and public methods:

- Like public methods, properties protect private data from outside access.
- Like fields, property names are used in the same way variable names are used.

You create properties, the syntax in your client programs becomes more natural and easier to understand.

Properties have accessors that specify the statements that execute when a class's fields are accessed. Specifically, properties contain set accessors for setting an object's fields and get accessors for retrieving the stored values. Figure 9-8 shows an Employee class in which a property named `IdNumber` has been defined in the shaded area.

```cs
class Employee
{
    private int IdNumber;
    get
    {
        return IdNumber;
    }
    set
    {
        IdNumber = value;
    }

    public void WelcomeMessage()
    {
        WriteLine("Welcome from Employee {0}", IdNumber);
        WriteLine("How can I help you?");
    }
}
```

Figure 9-8 Employee class with defined property

# Creating Properties

A property declaration resembles a variable declaration; it contains a modifier, data type, and an identifier. It also resembles a method in that it is followed by curly braces that contain statements. By convention, a property identifier is the same as the field it manipulates, except the first letter is capitalized. The field that supports a property is its backing field. Be careful with capitalization of properties. For example, within a get accessor for `IdNumber`, if you return the `IdNumber` instead of the backing field (`idNumber`), you initiate an infinite loop—the property continuously accesses itself.

The IdNumber property in Figure 9-8 contains both get and set accessors defined between curly braces; a property declaration can contain a get accessor, a set accessor, or both. When a property has a set accessor, programmers can say the property can be written to. When it has a get accessor, the property can be read from. When a property has only a get accessor (and not a set accessor), it is a readonly property. In C#, the get and set accessors are often called the getter and setter, respectively.

In the `Welcome()` method in Figure 9-8, the property is displayed. Alternatively, this method could continue to use the `IdNumber` field (as in Figure 9-3) because the method is a member of the same class as the field. Programmers differ on whether a class should use a field or a property to access its own methods. One popular position is that if get and set accessors are well designed, they should be used everywhere, even within a class. Sometimes, you want a field to be readonly, so you do not create a set accessor. In such a case, you can use the field (with the lowercase identifier) by convention within class methods.

Throughout this book you have seen keywords displayed in boldface in the program figures. The words get, set, and value are not C# keywords—for example you could declare a variable named within a C# program. However, within a property, set, and value have special meanings and are not allowed to be declared as identifiers. In the Visual Studio Development Environment, these three appear in blue properties, but in black elsewhere. Identifiers that act like keywords in specific circumstances are contextual keywords. C# has 13 contextual keywords: as, async, await, dynamic, global, remove, set, value, var, where, and yield.

Each accessor looks like a method, except that parentheses are not included in the identifier. A set accessor acts like a method that accepts a parameter and assigns it to a variable. However, it is not a method and you do not use parentheses with it. A get accessor returns the value of the field with the property, and the return type of the get accessor implies the type of the property in which it is contained.

When you use get and set accessors in a method, you do not use the assignment operator (=), and to get a value, you do use the set operator instead. To set a value, you simply use the property name. For example, if you declare an Employee `myChef`, you can assign an `IdNumber` as simply as you would a variable, as in the following:

```cs
Employee myChef = new Employee();
myChef.IdNumber = 2345;
```
