
## Software Engineering Observation 10.14

> If a readonly instance variable is initialized to a constant only in its declaration, it's not necessary to have a separate copy of the instance variable for every object of the class. The variable should be declared const instead. Constants declared with const are implicitly static, so there will only be one copy for the entire class.

## C# 6 Getter-Only Auto-Implemented Properties and readonly

Section 8.6.1 introduced C# 6's getter-only auto-implemented properties. When an auto-implemented property has only a get accessor, the property can be used only to read the value, so the compiler implicitly declares the corresponding private instance variable as readonly. Getter-only auto-implemented properties can be initialized in their declarations or in constructors.

## 10.11 Class View and Object Browser

Now that we have introduced key concepts of object-oriented programming, we present two Visual Studio features that facilitate the design of object-oriented apps—the Class View and the Object Browser.

### 10.11.1 Using the Class View Window

The Class View displays the fields, methods and properties for all classes in a project. Select View > Class View to display the Class View as a tab in the same position within the IDE as the Solution Explorer. Figure 10.12 shows the Class View for the Time1 project of Fig. 10.1 (class Time1) and Fig. 10.2 (class Time1Test).

![](img/3f5ef6be1748bb746e5f71a483bba4d0_324_0.png)

Fig. 10.12 | Class View of class Time1 (Fig. 10.1) and class Time1Test (Fig. 10.2).

The view follows a hierarchical structure, positioning the project name (Time1) as the root and including a series of nodes that represent the classes, variables, methods and properties in the project. If a appears to the left of a node, that node can be expanded to show other nodes. If a appears to the left of a node, that node can be collapsed. According to the Class View, project Time1 contains class Time1 and class Time1Test as children. When class Time1 is selected, the class's members appear in the lower half of the window. Class Time1 contains methods SetTime, ToString and ToUniversalString, indicated by purple boxes and public properties Hour, Minute and Second, indicated by wrench icons

If a class has any private members, those members' icons contain small padlocks. Both class Time1 and class Time1Test contain the Base Types node. If you expand this node, you'll see class Object in each case, because each class inherits from class System.Object— we discuss this concept in Chapter 11.

### 10.11.2 Using the Object Browser

Visual Studio's Object Browser lists all classes in the .NET library. You can use the Object Browser to learn about the functionality provided by a specific class. To open the Object Browser, select View > Object Browser. Figure 10.13 depicts the Object Browser when the user navigates to the Math class in namespace System. To do this, we expanded the node for mscorlib (Microsoft Core Library) in the upper-left pane of the Object Browser, then expanded its subnode for System. The most common classes from the System namespace, such as System.Math, are in mscorlib.

![](img/3f5ef6be1748bb746e5f71a483bba4d0_325_0.png)

Fig. 10.13 | Object Browser for class Math.

The Object Browser lists all methods provided by class Math in the upper-right pane—this offers you "instant access" to information regarding the functionality of various objects. Clicking the name of a member in the upper-right pane displays a description of that member in the lower-right pane. The Object Browser can be used to quickly learn about a class or one of its methods. You also can view the complete description of a class or a method in the online documentation by selecting the type or member in the Object Browser and pressing F1.

## 10.12 Object Initializers

Object initializers allow you to create an object and initialize its public properties (and public instance variables, if any) in the same statement. This can be useful when a class does not provide an appropriate constructor to meet your needs, but does provide a constructor that can be called with no arguments and properties that you can use to set the class's data. The following statements demonstrate object initializers using the class Time2 from Fig. 10.5.

```
// create a Time2 object and initialize its properties
var aTime = new Time2 {Hour = 14, Minute = 30, Second = 12};

// create a Time2 object and initialize only its Minute property
var anotherTime = new Time2 {Minute = 45};
```

The first statement creates a Time2 object (aTime), initializes it with class Time2's constructor that can be called with no arguments, then uses an object initializer to set its Hour, Minute and Second properties. Notice that new Time2 is immediately followed by an object initializer list—a comma-separated list in curly braces ({ }) of properties and their values. Each property name can appear only once in the object-initializer list. The object initializer executes the property initializers in the order in which they appear.

The second statement creates a new Time2 object (anotherTime), initializes it with class Time2's constructor that can be called with no arguments, then sets only its Minute property using an object initializer. When the Time2 constructor is called with no arguments, it initializes the time to midnight. The object initializer then sets each specified property to the supplied value. In this case, the Minute property is set to 45. The Hour and Second properties retain their default values, because no values are specified for them in the object initializer.

## 10.13 Operator Overloading; Introducing struct

Method-call notation can be cumbersome for certain kinds of operations, such as arithmetic. In these cases, it would be convenient to use C#'s rich set of built-in operators instead. This section shows how to create operators that work with objects of your own types—via a process called operator overloading.

You can overload most operators. Some are overloaded more frequently than others, especially the arithmetic operators, such as + and -, where operator notation is more natural than calling methods. For a list of overloadable operators, see

https://msdn.microsoft.com/library/9edha89s

### 10.13.1 Creating Value Types with struct

To demonstrate operator overloading, we’ll define type ComplexNumber (Section 10.13.2). Complex numbers have the form

$\mathrm{realPart} + \mathrm{imaginaryPart} * i$

where i is √−1. Like integers and floating-point numbers, complex numbers are arithmetic types that are commonly used in calculations. As you know, C#’s simple numeric types are value types. To mimic the simple numeric types, we’ll define ComplexNumber as a value type by using a struct (short for “structure”) rather than a class. C#’s simple types like int and double are actually aliases for structures that are defined by the struct System.Int32, a long by System.Int64, a double by System.Double and so on. The operator overloading techniques shown in Section 10.13.2 also can be applied to classes.

### When to Declare a struct Type

Microsoft recommends using classes for most new types, but recommends a struct if:

- the type represents a single value—a complex number represents one number that happens to have a real part and an imaginary part.
- the size of an object is 16 bytes or smaller—we’ll represent a complex number’s real and imaginary parts using two doubles (a total of 16 bytes).

For the complete list of struct recommendations, see

https://msdn.microsoft.com/library/ms229017

### 10.13.2 Value Type ComplexNumber

Value type ComplexNumber (Fig. 10.14) overloads the plus (+), minus (−) and multiplication (*) operators to enable programs to add, subtract and multiply instances of class ComplexNumber using common mathematical notation. Lines 9–10 define getter-only auto-implemented properties for the ComplexNumber’s Real and Imaginary components.

```csharp
// Fig. 10.14: ComplexNumber.cs
// Value type that overloads operators for adding, subtracting
// and multiplying complex numbers.
using System;

public struct ComplexNumber
{
   // read-only properties that get the real and imaginary components
   public double Real { get; }
   public double Imaginary { get; }

   // constructor
   public ComplexNumber(double real, double imaginary)
   {
```

**Fig. 10.14** | Value type that overloads operators for adding, subtracting and multiplying complex numbers. (Part 1 of 2.)
