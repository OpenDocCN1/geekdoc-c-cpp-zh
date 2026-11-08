
![](img/43c5f409f9b17790a628c4b4df854b61_524_0.png)

## 17 Basic of C#

| If you need information on: | See page: |
|---|---:|
| C# Hello World Program | 484 |
| Data Type | 487 |
| Declaration of Variables | 489 |
| Expression, Operators, and Operator Precedence | 490 |
| Type Casting | 492 |
| Arrays | 494 |
| Strings | 498 |
| Structure | 505 |
| Collection | 508 |
| Reference Type | 513 |
| Value Type | 515 |
| Flow Control Statements | 516 |
| Scope of Variables | 525 |
| Parameter Passing | 527 |
| Named and Optional Arguments | 530 |
| Namespace | 532 |

C# (pronounced as C Sharp) is the first component-oriented language in the family of C/C++. It is called component-oriented language, as its basic unit of coding is class. C# is a general-purpose, advanced, object-oriented programming language that borrows the main concepts from other languages. However, C# is much more similar to Java based on the functionalities it provides. We can write C# code in any text editor and compile it with the help of the C# compiler, but this programming language is mainly used in the .NET environment. Therefore, for developing a Web application or Web Service, the most commonly used programming language is C#. Sometimes, it is also called the .NET language, as C# was designed in parallel with the design of the .NET environment.

C# comes as a response to Java from Microsoft. The lead designers of this language are Anders Hejlsberg and Scott Wiltamuth. C# was launched officially in the year 2000 and its name was inspired by the musical note C#, which represents a step above to C/C++. However, this language has no intention to compete with C or any assembly level language.

If we consider the language performance, then C# requires no performance cost as compared to Java. We just need to install the .NET Framework and then it can be used for creating software components, Web pages, and Web services. C# enhances the productivity of programmers as well as the software robustness. In addition, programmers can easily adapt to C# if they are familiar with C++ and Java.

In this chapter, we mainly discuss about the basic functionality of C#. We start the chapter by writing a small program that helps in understanding the code structure of C#. After that, we get to learn about data types, variable declaration, expression, operators, and operator precedence in C#. In addition, we discuss about type casting, arrays, strings, structures, collections, reference types, and value types. This chapter also explains the use of flow control statements, scope of variables, parameter passing, and named and optional arguments with the help of programs. Towards the end, we learn about namespace, which provides a collection of classes, interfaces, structures, and enumerators.

Let's begin the chapter by writing a C# program that helps in understanding the general structure of C#.

### C# Hello World Program

The structure of a C# program is somewhat similar to the Java and C++ programs. Therefore, a C# program also begins with the namespace references that are given by using the directive "using". In addition, the whole code body resides inside the multiple class definitions. Note that at least one class must contain a method called Main(), which is the main entry point of the compiler to compile the code. Let's now write a simple C# program called HelloWorld.cs that only prints "Hello World!!!!!!!!!!" as an output on the console. Listing 17.1 shows the code of the HelloWorld.cs program:

### Listing 17.1: Showing the Code of HelloWorld.cs Program

```csharp
using System;

namespace HelloWorld
{
    class Program
    {
        public static void Main()
        {
            Console.WriteLine("Hello world!!!!!!!!!!");
        }
    }
}
```

After the compilation of the preceding program, the console window will show the output, as shown in Figure 17.1:

![](img/43c5f409f9b17790a628c4b4df854b61_526_0.png)

### Figure 17.1: Showing the Output of the HelloWorld.cs Program

Let’s now refer to Figure 17.2 to better understand the code structure of C#:

![](img/43c5f409f9b17790a628c4b4df854b61_526_1.png)

### Figure 17.2: Showing the Structure of C# Code

According to Figure 17.2, a C# program can consist of multiple files among which one class file should contain the Main() method that calls a method of some other class to execute the desired work. Each class contains a list of namespaces; however, the System namespace should be written at the first place in the class file, as this is the main namespace of C# language. Note that a class file may contain more than one class definition. However, for simplicity, we can consider one class per class file. Listing 17.2 shows an example of C# code that handles multiple class files:

### Listing 17.2: Showing the C# Code that Handles Multiple Class Files

Program.cs

```csharp
using System;
namespace Program
{
    class Program
    {
        public static void Main()
        {
            Addition addition = new Addition(10, 30);
            Console.WriteLine("The result of addition is {0}", addition.Add());
        }
    }
}
```

Addition.cs

```csharp
using System;
namespace Addition
{
    class Addition
    {
        public int item1 = 0;
        public int item2 = 0;

        public Addition(int a, int b)
        {
            this.item1 = a;
            this.item2 = b;
        }
        public int Add()
        {
            int result = this.item1 + this.item2;
            return result;
        }
    }
}
```

As shown in Listing 17.2, a class named Addition is written for the addition operation; whereas, the class named Program is written to execute the addition operation. The Program.cs file contains the Main() method that executes the addition operation by declaring the object of the Addition class. To execute the code, we need to separately compile these two class files to get the desired output. Although we have written the classes in the two separate files, these classes can also be incorporated in a single class file. This eases the compilation process, as only one single file needs to be compiled for this. Listing 17.3 shows the C# code that handles multiple classes in a single class file:

### Listing 17.3: Handling Multiple Classes in a Single Class File

```csharp
using System;
namespace Program
{
    class Program
    {
        public static void Main()
        {
            Addition addition = new Addition(10, 30);
            Console.WriteLine("The result of addition is {0}", addition.Add());
        }
    }
    class Addition
    {
        public int item1 = 0;
        public int item2 = 0;

        public Addition(int a, int b)
        {
            this.item1 = a;
            this.item2 = b;
        }
        public int Add()
        {
            int result = this.item1 + this.item2;
            return result;
        }
    }
}
```

In Listing 17.3, we have defined the two classes, named Program and Addition within the Program namespace. In the Addition class, the addition operation took place and in the Program class, the Main() method is called where two numbers 10 and 30 are added and then the result on the console is printed.

Let's now discuss the various data types in C#.

### Data Type

C# is known as a strongly typed language. A language is said to be strongly typed when every variable and object have a declared type. Therefore, whenever we declare an object or a variable in C#, it must have a declared type.

In C#, three kinds of data types exist that are given as follows:

- Built-in data types
- User-defined data types
- Anonymous type

Let's learn about these data types in detail starting with the built-in data types.

### Built-In Data Types

Built-in data types come under the System namespace, which is the root namespace of all the other namespaces in the .NET Framework. Some of the basic built-in data types are int, char, and bool. All these data types are objects of a class. In the .NET Framework, the root data type is the object data type. Table 17.1 represents a list of built-in data types in C#:

| Class Name | Data Type | Description |
|---|---|---|
| Category: Integer | | |
| Byte | byte | Represents 8-bit unsigned integer |
| SByte | sbyte | Represents 8-bit signed integer |
| Int16 | short | Represents 16-bit signed integer |
| Int32 | int | Represents 32-bit signed integer |
| Int64 | long | Represents 64-bit signed integer |
| UInt16 | ushort | Represents 16-bit unsigned integer |
| UInt32 | uint | Represents 32-bit unsigned integer |
| UInt64 | ulong | Represents 64-bit unsigned integer |
| Category: Floating Point | | |
| Single | float | Represents a 32-bit (single precision) floating point |
| Double | double | Represents a 64-bit (double precision) floating point |
| Category: Logical | | |
| Boolean | bool | Represents a true-false Boolean value |
