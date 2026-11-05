
## C# Platform

- 7. Visual Studio supports VB, VC++, C++, VBScript, JScript and C#. All of these languages provide access to the Microsoft .NET platform.
- 8. .NET platform includes a Common Execution Engine and a rich class library.
- 9. Microsoft’s Common Language Runtime (CLR) accommodates more than one language such as C#, VB.NET, JScript, ASP.NET, C++.
- 10. The steps followed for code execution is, Source code --> Intermediate Language code (IL) --> (JIT Compiler) Native code.
- 11. The built-in classes and data types are common to all of the .NET languages.

## C# can do

- 12. Using C# one can develop Console application, Windows application, Web application.
- 13. C# simplifies programming through its use of Extensible Markup Language (XML) and Simple Object Access Protocol (SOAP). This allows access to a programming object or method without requiring the programmer to write additional code for each step.

## C# being simple

- 14. There are no pointers in C#.
- 15. No direct memory manipulations are supported because generally they are unsafe in terms of storage access.
- 16. "::" or "->" operators are not used in C#.

## C# memory management

- 17. Automatic memory management and garbage collection is supported by .NET Framework. C# by default inherits these features of its platform.
- 18. There are various required ranges of the primitive data types like Integer, Floats etc.
- 19. Boolean values are pure true or false values in C#. Numeric values 0 and 1 are not used for true and false. Therefore, errors of "=" operator and "==" operator is not encountered.
- 20. Operator "==" is used for comparison operation and operator "=" is used for assignment operation.

## C# is latest

- 21. C# has followed current trends and is very powerful in terms of interoperability, scalability, robustness and web development.
- 22. It includes built-in support for converting any application component into a web service that can be invoked over the internet from any application running on any platform.

## C# follows object-oriented paradigm

- 23. Data abstraction, data encapsulation, inheritance, polymorphism all features are supported in C# making it complete object-oriented language.
- 24. C# has introduced structures (struct) which enable the primitive types (int, float, double) to become objects.

## C# is type safe

- 25. Unsafe casting like converting Double to a Boolean is unsupported in C#.
- 26. Automatic compiler initializations are supported in C#, like, value types (primitive types) are initialized to zeros and reference types (objects and classes) are initialized to null.
- 27. In C# arrays are zero-based indexed. Array bounds are checked.
- 28. C# allows for checking the overflow of types.

## C# is interoperable

- 29. C# has complete native support for the COM and Windows-based applications.
- 30. C# do allow restricted use of native pointers for supporting applications that are using pointers. C# allows the users to use pointers as unsafe code blocks to manipulate old code.
- 31. C# has built-in support for implementation of IUnknown and other COM interfaces.
- 32. Components from VB.NET and other managed code languages can directly be used in C#.

## C# is scalable

- 33. .NET platform has introduced assemblies which are self-describing by means of their manifest files. These manifest files establish the assembly identity, version, culture and digital signature. Also, assemblies need not to be registered anywhere.
- 34. If one needs to scale any application, then it can be done just by deleting the old files and updating them with new ones. There is no need of registration of dynamic-link library.

## C# is updatable

- 35. A big error-prone task in the application's life is its maintenance. Updating software components is a crucial and highly time-bound task. The revisions made to the code can affect the existing program. C# supports the concept of versioning as the language feature.
- 36. By the language itself, there is a native support for interfaces and method overriding which enables complex frameworks to be developed and evolved over the time.

## 1.3 OOP Concept

### Concept

- 1. Object Oriented Programming (*OOP*) is a design philosophy. *Object-Oriented Programming (OOP)* uses a different set of programming languages than old procedural programming languages (*C, Pascal, etc.*). Reusability is attained due to a bundle of self sustainable thing (the ‘object’). Due to ‘object’ concept four main object-oriented programming concepts have raised.
- 2. Let a ‘hand’ be a class. A human body has two objects of the type *‘hand’*, named “left hand” and “right hand”. Their main functions are controlled by a set of electrical signals sent through the shoulders (which acts as an interface between body and hand). The hand is a well-architected class. By changing little properties, the hand is being reused to create the left hand and the right hand.
- 3. Object Oriented Programming (OOP) is a programming paradigm (a programming thought process) wherein programs are organized around objects and data rather than action and logic.
- 4. OOP allows decomposition of a problem into a number of entities called objects and then builds data and functions around these objects.
- 5. OOP Features

### 1. Class

- 1. A class is the core of any modern Object Oriented Programming language such as C#. In OOP languages it is mandatory to create a class for representing data.
- 2. A class act as a blueprint of an object that contains variables for storing data and functions to perform operations on the data.
- 3. A class does not take any memory space as it is only a logical representation of data.
- 4. Creating Class - To create a class, the keyword "class" is used, followed by the class name, as shown below,

### Example

```csharp
class Book
{
}
```

### 2. Object

- 1. An object is an instance of a class. Object is a basic run-time entity of an object oriented system. It would represent actual place, person, book or any item that the program is dealing with.
- 2. An object is a bundle of software of related variable and methods.
- 3. An object is a real-world entity that keeps together property states and behaviors.
- 4. To make use of the Class, one must create a variable for the class, which is termed as object.
- 5. Object is called as an instance of Class and its starting address is stored in the object when it is instantiated. In C# language, Object can be instantiated as follows,

### Example

```csharp
Book objBook = new Book();
```

### 3. Abstraction

- 1. Abstraction is, "To represent the essential feature without representing the background details."
- 2. Abstraction tries to focus on what the object does instead of how it does it.
- 3. Abstraction provides a way to generalize the view of classes or objects by providing relevant information about them.
- 4. Abstraction is the process of providing only essential information to the outside real world and hiding overall background details to present an object.
- 5. It relies on the separation of interface and implementation.
- 6. Abstraction solves the problem at the design level.
- 7. Abstraction is a outer layout, used in terms of design.
- 8. For example : An external of a microwave oven, it has a display screen with keypad buttons to set temperature, timer etc.

### Example of Abstraction

```csharp
public class Car
{
    public int mileage = 65;
    public string color = "Red";
    private string engineformula = "m*n";

    // It's public – so accessible outside class
    public int GetMileage()
    {
    }

    // It's public – so accessible outside class
    public string GetColor()
    {
    }

    // It's private – so not accessible outside class
    private string GetEngineMakeFormula()
    {
    }

    // It's public – so accessible outside class
    public string DisplayMakeFormula()
    {
        // "GetEngineMakeFormula()" is private but accessible to this class only
        return GetEngineMakeFormula();
    }
}
```

As it can be seen from the above example that necessary methods and properties are exposed using *public* access modifier and rest of the methods and properties are hidden using *private* access modifier. This way abstraction is achieved in the applications.

### 4. Information Hiding

- 1. Information hiding concept restricts direct exposure of the data.
- 2. Data is accessed indirectly using safe mechanism so as to avoid unwanted handling of data.
- 3. Objects and their methods are used for data hiding implementation.

### 5. Encapsulation

- 1. Wrapping up a data member and a method together into a single unit (in other words class) is called Encapsulation.
- 2. Encapsulation is like enclosing material in a capsule. That is enclosing the related operations and data related to an object into that object.
- 3. For example sack can encapsulate bottle, tiffin, files, laptop etc. In an object one encapsulates data members and functions working around data members.

### Example

```csharp
class Sack
{
    tiffin;
    Bottle;
    files;
    laptop;
    ReadFile();
}
```
