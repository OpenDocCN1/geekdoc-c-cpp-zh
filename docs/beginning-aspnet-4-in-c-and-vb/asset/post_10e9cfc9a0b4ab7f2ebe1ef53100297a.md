
## Objects and Types

### WHAT'S IN THIS CHAPTER?

- The differences between classes and structs
- Class members
- Passing values by value and by reference
- Method overloading
- Constructors and static constructors
- Read-only fields
- Partial classes
- Static classes
- The `Object` class, from which all other types are derived

So far, you've been introduced to some of the building blocks of the C# language, including variables, data types, and program flow statements, and you have seen a few very short complete programs containing little more than the `Main()` method. What you haven't really seen yet is how to put all these together to form a longer, complete program. The key to this lies in working with classes — the subject of this chapter. Note that we cover inheritance and features related to inheritance in Chapter 4, "Inheritance."

> > This chapter introduces the basic syntax associated with classes. However, we assume that you are already familiar with the underlying principles of using classes — for example, that you know what a constructor or a property is. This chapter is largely confined to applying those principles in C# code.

### CLASSES AND STRUCTS

Classes and structs are essentially templates from which you can create objects. Each object contains data and has methods to manipulate and access that data. The class defines what data and functionality each particular object (called an instance) of that class can contain. For example, if you have a class that represents a customer, it might define fields such as `CustomerID`, `FirstName`, `LastName`, and `Address`, which you will use to hold information about a particular customer. It might

```
}
public static int GetSquareOf(int x)
{
    return x*x;
}
public static double GetPi()
{
    return 3.14159;
}
}
```

code snippet MathTest.cs

Running the MathTest example produces these results:

```
Pi is 3.14159
Square of 5 is 25
Value field of math variable contains 30
Square of 30 is 900
```

As you can see from the code, the MathTest class contains a field that contains a number, as well as a method to find the square of this number. It also contains two static methods, one to return the value of pi and one to find the square of the number passed in as a parameter.

Some features of this class are not really good examples of C# program design. For example, GetPi() would usually be implemented as a const field, but following good design here would mean using some concepts that we have not yet introduced.

### Passing Parameters to Methods

In general, parameters can be passed into methods by reference or by value. When a variable is passed by reference, the called method gets the actual variable — so any changes made to the variable inside the method persist when the method exits. But, when a variable is passed by value, the called method gets an identical copy of the variable — which means any changes made are lost when the method exits. For complex data types, passing by reference is more efficient because of the large amount of data that must be copied when passing by value.

In C#, all parameters are passed by value unless you specifically say otherwise. However, you need to be careful in understanding the implications of this for reference types. Because reference type variables hold only a reference to an object, it is this reference that will be copied, not the object itself. Hence, changes made to the underlying object will persist. Value type variables, in contrast, hold the actual data, so a copy of the data itself will be passed into the method. An int, for instance, is passed by value to a method, and any changes that the method makes to the value of that int do not change the value of the original int object. Conversely, if an array or any other reference type, such as a class, is passed into a method, and the method uses the reference to change a value in that array, the new value is reflected in the original array object.

Here is an example, ParameterTest.cs, which demonstrates the following:

```
using System;
namespace Wrox
{
    class ParameterTest
    {
        static void SomeFunction(int[] ints, int i)
        {
            ints[0] = 100;
            i = 100;
```

Constructors follow the same rules for overloading as other methods (that is, you can provide as many overloads to the constructor as you want, provided they are clearly different in signature):

```
public MyClass()  // zero-parameter constructor
{
    // construction code
}
public MyClass(int number)  // another overload
{
    // construction code
}
```

Note, however, that if you supply any constructors that take parameters, the compiler will not automatically supply a default one. This is done only if you have not defined any constructors at all. In the following example, because a one-parameter constructor is defined, the compiler assumes that this is the only constructor you want to be available, so it will not implicitly supply any others:

```
public class MyNumber
{
    private int number;
    public MyNumber(int number)
    {
        this.number = number;
    }
}
```

This code also illustrates typical use of the this keyword to distinguish member fields from parameters of the same name. If you now try instantiating a MyNumber object using a no-parameter constructor, you will get a compilation error:

```
MyNumber numb = new MyNumber();  // causes compilation error
```

We should mention that it is possible to define constructors as private or protected, so that they are invisible to code in unrelated classes too:

```
public class MyNumber
{
    private int number;
    private MyNumber(int number)  // another overload
    {
        this.number = number;
    }
}
```

This example hasn’t actually defined any public or even any protected constructors for MyNumber. This would actually make it impossible for MyNumber to be instantiated by outside code using the new operator (though you might write a public static property or method in MyNumber that can instantiate the class). This is useful in two situations:

- If your class serves only as a container for some static members or properties and therefore should never be instantiated
- If you want the class to only ever be instantiated by calling some static member function (this is the so-called class factory approach to object instantiation)

### Static Constructors

One novel feature of C# is that it is also possible to write a static no-parameter constructor for a class. Such a constructor will be executed only once, as opposed to the constructors written so far, which are instance constructors that are executed whenever an object of that class is created.

```
class MyClass
{
    static MyClass()
}
```

![](img/d7d2ffa0a76feaab821930e95daace93_138_0.png)

```
    this.nWheels = nWheels;
}

public Car(string description): this(description, 4)
{
}
// etc
```

In this context, the `this` keyword simply causes the constructor with the nearest matching parameters to be called. Note that any constructor initializer is executed before the body of the constructor. Say that the following code is run:

```
Car myCar = new Car("Proton Persona");
```

In this example, the two-parameter constructor executes before any code in the body of the one-parameter constructor (though in this particular case, because there is no code in the body of the one-parameter constructor, it makes no difference).

A C# constructor initializer may contain either one call to another constructor in the same class (using the syntax just presented) or one call to a constructor in the immediate base class (using the same syntax, but using the keyword `base` instead of `this`). It is not possible to put more than one call in the initializer.

### readonly Fields

The concept of a constant as a variable that contains a value that cannot be changed is something that C# shares with most programming languages. However, constants don’t necessarily meet all requirements. On occasion, you may have some variable whose value shouldn’t be changed, but where the value is not known until runtime. C# provides another type of variable that is useful in this scenario: the `readonly` field.

The `readonly` keyword gives a bit more flexibility than `const`, allowing for situations in which you might want a field to be constant but also need to carry out some calculations to determine its initial value. The rule is that you can assign values to a `readonly` field inside a constructor, but not anywhere else. It’s also possible for a `readonly` field to be an instance rather than a static field, having a different value for each instance of a class. This means that, unlike a `const` field, if you want a `readonly` field to be static, you have to declare it as such.

Suppose that you have an MDI program that edits documents, and, for licensing reasons, you want to restrict the number of documents that can be opened simultaneously. Now assume that you are selling different versions of the software, and it’s possible that customers can upgrade their licenses to open more documents simultaneously. Clearly, this means you can’t hard-code the maximum number in the source code. You’d probably need a field to represent this maximum number. This field will have to be read in — perhaps from a registry key or some other file storage — each time the program is launched. So your code might look something like this:

```
public class DocumentEditor
{
    public static readonly uint MaxDocuments;

    static DocumentEditor()
    {
        MaxDocuments = DoSomethingToFindOutMaxNumber();
    }
}
```

In this case, the field is static, because the maximum number of documents needs to be stored only once per running instance of the program. This is why it is initialized in the static constructor. If you had an instance `readonly` field, you would initialize it in the instance constructor(s). For example, presumably each document you edit has a creation date, which you wouldn’t want to allow the user to change (because that would be rewriting the past!). Note that the field is also public — you don’t normally need to make `readonly` fields private, because by definition they cannot be modified externally (the same principle also applies to constants).
