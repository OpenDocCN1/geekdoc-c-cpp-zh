# C# 编程：计算机编程初学者指南：学习 C# 基础 (Coding, C 编程, Java 编程, C# 编程, JavaScript, Python, PHP)

## 引言

首先，感谢您购买本书《编程：计算机编程入门：学习C#基础》。C# 由微软在其 .NET 计划下开发。

C#（发音为 C Sharp）是一种编程语言。它是一种多范式编程语言，因为它支持包括面向对象范式在内的多种编程范式。因此，在为手头任务选择编程风格时，你享有极大的灵活性。此外，对于希望迈入计算机编程广阔世界的初学者来说，C# 被认为是一种易学的语言。

学习C#将为你带来众多机会。从C#出发，你可以退一步学习强大的C语言，然后再学C++。掌握C#还能让你通过 .NET 平台掌握 Web 开发所需的技能。此外，如果你计划未来为微软生态系统开发产品，这门语言也很有帮助。

你是不是感到不知所措？对于一个初学者来说，这可能信息量很大。但你不必过于担心。本书将帮助你获得成为一名C#程序员所需的基础知识。你将学习一些很棒的新术语，甚至一些程序。你会接触到这门语言中使用的一些术语和函数。简而言之，你将得到全面的准备，从而能够学习高级课程，成为一名顶尖的程序员。

现在，让我们开始学习C#吧！

## 第1章：C#简介

在微软最初开发 .NET 框架时，程序员必须借助 Simple Managed C（一种托管代码编译器系统）来编写类库。然而，使用 C 存在一些问题。因此，C# 被开发为一种新语言来克服这些问题。

C# 被专门设计得简单而现代。它是一种面向对象、通用的编程语言。如果你已经熟悉编程，你会很容易发现 C# 借鉴了其他多种编程语言的一系列关键概念，其中最著名的是 Java。

### .NET框架的重要性

从理论上讲，C# 可以被编译为机器代码。尽管如此，这门语言在现实生活中几乎总是与 .NET 框架一起使用。因此，你需要确保运行用 C# 编写的应用程序的计算机上已安装 .NET 框架。

.NET 框架与大量编程语言兼容。然而，与这个框架最常关联的是 C#。在某些圈子里，它甚至被称为“THE .NET 语言”。这很可能是因为该框架和该语言是同时开发的。

### 开始C#编程需要什么？

在开始编写 C# 程序之前，你需要先处理一些事情。请确保计算机上已安装以下程序。

- .NET框架软件开发工具包（SDK）
- 编辑器

仅此而已。这是开始用 C# 编程所需的仅有的两样东西。可用的编辑器很多。你甚至可以使用记事本或 DOS 编辑器，但稍后会有更多介绍。尽管如此，如果你安装以下可选程序中的任意一个，将更有利于你的学习曲线。

- Visual C# .NET
- Visual C++ 6.0。它包含在 Microsoft Visual Studio 6.0 软件包中。

你的第一步应该是在计算机上安装 .NET SDK。你可以轻松地从微软官方网站下载该程序。你还将获得该程序的完整文档。安装此工具包后，你将能够编译和执行 C# 源代码。这得益于工具包内置的命令行编译器以及运行时即时（JIT）编译器。如果你以前接触过 Java，你可以将它们视为类似于 Java 开发工具包中的 Java 编译器和 Java 解释器。

### 关于编辑器

编辑器是用于编写源代码的程序。在这方面，C# 非常灵活，几乎可以用任何文本编辑器来编写。即使是 Windows 中自带的基本记事本也是个不错的选择。编译时，你可以轻松使用 .NET 框架中的命令行编译器 csc.exe。

在使用 .NET SDK 开发 C# 程序时，记事本是一个常见的选择。另一方面，它并不是最好的编辑器，尤其是对初学者而言。毕竟，记事本缺少一些有用的功能，例如代码编号和语法着色。

这就是为什么许多开发者更喜欢使用集成开发环境（IDE）。有不少



options available from Microsoft, the best of which is Visual Studio. This program can be used for working on all the aspects of the .NET framework. This is certainly a highly advanced program and is available in a range of editions. The complete Visual Studio does cost quite a bit and may be too advanced even for hobbyists.

On the release of the .NET framework, Express versions of the product were introduced by Microsoft. These versions are meant for hobby programmers and those who are just starting with the .NET framework. The Express versions will only work for a single language. They may not have the most advanced features of Visual Studio, but they are free. They are also quite easy to use for learning the language of your choice which is C# in this case.

There are some other third-party editors available in the market. However, for this book, we will be using Visual C# Express for writing the code. You must remember that the codes will remain the same irrespective of the editor you are using.

## Chapter 2

### Hello World: Writing Your First C# Program

If you have learned or dabbled in any programming language previous to C#, you will be familiar with “Hello, world!” This is a basic example that demonstrates the programming language in action. This is exactly what you will be learning in this chapter.

This programming example will illustrate the fundamentals of the programming language. You will come across a few functions and classes that you will surely be using later while writing more advanced codes.

### Starting a New Project

To start a new C# project, you should first open Visual C# Express. In the File menu, select the New Project option. The project dialog will open where you should choose the Console application. This will be the most basic application type that you can find on a system running Windows. Click on the Ok option so that Visual C# Express can create the new project for you.

You will also notice the creation of a file that has been named as Program.cs. This will be the application file where you will be writing the code. You will notice that the file already has a few lines of code as shown below.

```
using System;

using System.Collections.Generic;

using System.Text;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

These lines of code will most certainly work, but the end result is nothing at all. You can run the application if you want by pressing the F5 key. This will cause Visual C# Express to compile and then execute your code. On execution, a black

window will be launched which will then close again. This is simply because the application does not have any other functions to perform.

In order to make this program actually do something, you need to insert a couple of lines of code. You should enter the following two lines inside the last set of {}.

```
Console.WriteLine ("Hello, world!");
```

```
Console.ReadLine ();
```

On entering the lines, your entire program should resemble the following.

```
using System;
using System.Collections.Generic;
using System.Text;
namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
```

```
Console.WriteLine("Hello, world!");
Console.ReadLine();
}
}
}
```

In order to run this program, you should press F5 again. If there are no mistakes, you will notice that the black window remains instead of closing. In the window, you will notice the message “Hello, world!” displayed. Of course, this is the phrase that you entered into the application.

There is a reason why C# is considered to be a very user-friendly programming language. That reason is that it is easy to understand much of the code even if you have never written programs in it before. You will easily notice this in the program that you just wrote.

### Understanding the ‘Hello, world!’ Program

The previous application was just an example of how you can write a program in C#. Of course, you need to understand as to how it actually worked and what does the code actually mean. This is what you will be learning in this section.

To understand the program, consider the ‘{’ and ‘}’ first. After all, they are repeated multiple times in the program. They are known as curly braces. In C#, these braces signify the start and

the end of a logical section of code. You will notice that these braces are often used in a range of other programming languages such as Java and C++ among others. As the example demonstrates, their main function is to bring together several lines of code that belong together.

```
using System;
```

```
using System.Collections.Generic;
```

```
using System.Text;
```

If you are using Visual C# Express, you will notice that the term ‘using’ has been highlighted in blue. This is actually a keyword, and its function is to import a namespace. A collection of classes is known as the namespace. It is the job of Classes to provide you with certain functionalities automatically.

When you are working on an advanced IDE such as Visual C# Express, the keyword, ‘using’ will end up creating parts of the trivial code in your stead. In this example, it was used for creating a class for you. It also imported the namespaces that are necessary or are expected to be used.

In this example, three namespaces have been imported into the program. Each of these namespaces contains some useful classes. The Console class has been used in this program, and it belongs to the System namespace.

You will also notice that the application gets its very own namespace as shown below.

### 'Namespace' ConsoleApplication1

This is now the primary namespace for this application. By default, any new classes created will become a part of it. It is possible to modify this and create other classes under another namespace. If you want to do so, you need to import this namespace into your application with the help of the ‘using’ statement.

For the next step, the class has to be defined. C# is an objected oriented language. As a result, all lines of code which actually performs something will have to be kept inside a class. For this example, the class has been named Program as shown below.

### 'Class' Program

It is possible to increase the number of classes in the same application. However, that was not necessary for this program. A class is capable of containing a number of methods, properties, and variables. However, that will be discussed later. In this program, there is only a single method which is declared as follows.

### 'Static void Main' (string [] args)

The first word of this line is static, and it is a keyword. It instructs the program to keep the method accessible without causing the class to instantiate. The void keyword tells the

program what should be returned by the program which in this case is nothing.

The word, Main, is simply the name given to this method. In this case, it serves as what is known as the entry-point of the application. In other words, this will be the first section of the code that will be executed in the program.

After the name of the method has been declared, it is possible to specify a set of arguments with the help of parentheses. In this example, args is the only argument used by the method.

The next two lines are the actual program. In the first line, the Console class is used to deliver the text as output by means of the ‘WriteLine’ command. Of course, the text is, in this case, ‘Hello, world!’ The second line reads the line of text shown in the console through the ‘ReadLine’ command.

The ReadLine command is essential as it allows the window to remain open. Without it, the application would simply run and end. The window will be closed before you can see the output. The main function of this command is to make the application wait for some input from the user. In this example, you will find that you can enter text after the text has been displayed. On pressing Enter, the window will close and, thereby, bring an end to the program.





With this, you will have successfully completed writing your very first program. You will have also learned a few functions and terms that you are going to need while writing C# programs.

## Chapter 3: Understanding Data Types and Variables

Whenever you are using a programming language, you are certain to come across data types. As C# is a strongly typed programming language, it is necessary for you to tell the compiler which data types you are going to use every time you want to declare a variable. Of course, variables are critical to any programming language.

### Introduction to Data Types

In C#, data types can be broadly classified into three types. They are discussed as follows.

- **Value Type:** These data types can be directly assigned a value, and they are derived from the System.ValueType class. As such, they contain the data directly. Some examples of value types are char, int, and bool.

- **Reference Type:** These data types do not have the actual data kept in a variable. Instead, they have a reference to the variables. That means that they actually refer to a specific memory location. It is possible to use multiple variables to refer to a specific memory location. In this case, if one variable changes the data present in the memory location, the other variables will automatically reflect the change. Some examples of reference types include string, dynamic, and object.

- **Pointer Types:** These data types actually store the memory address of some other type. If you are familiar with C++ or C, you will understand that the pointer types in C# will have the same capabilities as those of the pointer types in those programming languages.

### The Common Data Types

There are a wide variety of data types used in C#. Of course, some of them will be used more often than others when you start programming in earnest. As a result, it will benefit you greatly if you start learning about the most widely used data types. Here are some of them to help you get started.

**Bool:** This is one of the simplest data types available as it represents a Boolean value. As such, it can have only two values, either true or false. It is important to understand this type, especially when using logical operators such as the 'if' statement. By default, its value is false.

**Byte:** This data type represents an 8-bit integer that is unsigned. It has a range of 0 to 255 when it comes to storing numbers. By default, the value of this data type is 0.

**Int:** This is actually short for the integer which is a data type used for storing numbers that do not have decimals like the byte data type. However, unlike byte, int has a range of -2,147,483,648 to 2,147,483,647. If you are working with numbers, you are more likely than not to end up using this data type.

**Char:** This data type represents a 16-bit Unicode character, and it is used for storing only one character.

**String:** This can be said to be an upgraded version of the char data type as it can be used for storing text. That is, it can store multiple chars instead of a single one. In C#, this data type is immutable. In other words, after the creation of a string, it is never changed. If you use methods which can change a string, a new string is actually returned. The original one is not changed.

### An Introduction to Variables

Variables are crucial to programming. In any programming language, a variable is actually a storage location which has been associated with a name (referred to as an identifier) and it contains some quantity of information which may be unknown or known. This information is referred to as the value. The identifier is used for referencing the stored value. During runtime, the identifier can be linked to a value, but this value may change as the program is being executed.

In C#, variables are declared in the following syntax: `<data type> <name>;`

However, it is possible to assign a value to the variable at the same time that you are making it visible. In such cases, you need to use the following syntax in order to do so: `<visibility> <data type> <name> = <value>;`

Here is an example application that demonstrates the use of variables.

```csharp
using System;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            string firstName = "John";
            string lastName = "Doe";
            Console.WriteLine("Name: " + firstName + " " + lastName);
            Console.WriteLine("Please enter a new first name :");
            firstName = Console.ReadLine();

            Console.WriteLine("New name: " + firstName + " " + lastName);

            Console.ReadLine();
        }
    }
}
```

You will already recognize a few commands and statements from the earlier chapter. As such, let's concentrate on the variables.

In the program, two variables are declared first, and they have been defined as string type variables. A value is also assigned to the variables immediately in the same statement. Therefore, the two variables have been named as "firstName" and "lastName" and they contain the values, "John" and "Doe" respectively.

In the next statement, some text is sent as output to the console. For the output, the two variables have been used. In this case, the + characters have been used to bring together the various parts of the output text.

In the next section of the code, the user is requested to enter a new name. The input from the user is then recognized and read from the console by means of the ReadLine() method. The input is then assigned as the value of the variable, "firstName".

The next statement displays the value of the "firstName" variable to the user to denote that it has changed. This is one of the most common ways to change the value of any variable during runtime.

Now, you know the basics of data types and variables. You have also learned how to declare variables and assign values to them. You have even learned how to change a variable's value during runtime.

### Converting Datatypes

Type conversion is simply the conversion of one data type to another type. Another name for this process is type casting. It is an essential part of programming. As such, it is a good idea to get familiar with it as soon as possible.

In C#, there are two different forms of type conversion as follows.

Implicit type conversion: In this case, the conversions are executed in a type-safe manner by C#. For example, converting a smaller integral data type to a larger one will be an implicit type conversion. Another example is converting to base classes from derived classes.

Explicit type conversion: These are the conversions which are performed explicitly by the users with the help of the predefined functions. In order to perform an explicit conversion, a cast operator is a must.

Take a look at the following example to get a better understanding of explicit type conversions.

```csharp
using System;

namespace TypeConversionApplication
{
    class ExplicitConversion
    {
        static void Main(string[] args)
        {
            double d = 5673.74;
            int i;

            // cast double to int.
            i = (int)d;

            Console.WriteLine(i);
            Console.ReadKey();
        }
    }
}
```

On executing the code shown above, the following result is going to be produced.

```
5673
```

### The Type Conversion Methods Available In C#

There are quite a few type conversion methods that have already been built into C#.

- ToBoolean: A type will be converted to a Boolean value if possible.
- ToByte: A type will be converted to a byte.
- ToChar: A type will be converted to a single Unicode character if possible.
- ToDateTime: An integer type or string type will be converted to a date-time structure.
- ToDecimal: A floating point type or integer type will be converted into a decimal datatype.
- ToDouble: A type will be converted to a double type.
- ToInt16: A type will be converted into a 16-bit integer.





- `ToInt32`：将类型转换为 32 位整数。
- `ToInt64`：将类型转换为 64 位整数。
- `ToSByte`：将类型转换为有符号字节数据类型。
- `ToSingle`：将类型转换为单精度浮点数。
- `ToString`：将类型转换为字符串。
- `ToType`：将类型转换为指定类型。
- `ToUInt16`：将类型转换为无符号整数数据类型。
- `ToUInt32`：将类型转换为无符号长整型数据类型。
- `ToUInt64`：将类型转换为无符号大整数。

### 掌握常量和字面量

常量指的是程序执行期间无法以任何方式更改的固定值。这些固定值的另一个术语是字面量。任何基本数据类型都可以用作常量。示例包括字符常量、浮点常量、整数常量和字符串字面量。此外，还存在枚举常量。

实际上，常量与常规变量的处理方式相同，但有一个重大区别：常量一旦定义，其值就不能以任何方式更改。现在让我们逐一了解字面量和常量的各类形式。

### 整数字面量

在 C# 中，整数字面量可以是十进制常量或十六进制常量。进制由前缀指定。对于十六进制常量，使用前缀 `0X` 或 `0x`。十进制常量不使用前缀。

整数字面量还可以带有由 `L` 和 `U` 组合而成的后缀。`L` 表示长整数，`U` 表示无符号数。后缀可使用小写或大写。后缀的顺序没有规定。

请看以下整数字面量的示例。

```text
212    /* Legal */
215u   /* Legal */
0xFeeL /* Legal */
85     /* decimal */
0x4b   /* hexadecimal */
30     /* int */
30u    /* unsigned int */
30l    /* long */
30ul   /* unsigned long */
```

### 浮点字面量

这些字面量由整数部分、小数点、小数部分以及指数部分组成。浮点字面量可以表示为十进制形式或指数形式。

请看以下示例，以便更好地理解浮点字面量。

```text
3.14159     /* Legal */
314159E-5L  /* Legal */
510E        /* Illegal: incomplete exponent */
210f        /* Illegal: no decimal or exponent */
.e55       /* Illegal: missing integer or fraction */
```

如果使用十进制形式表示，必须记住插入小数点或指数。如果愿意，也可以同时使用两者。对于指数形式，必须插入整数部分或小数部分。两者也都可以使用。对于有符号指数，必须使用 `e` 或 `E` 来引入。

### 字符常量

这些字面量用单引号括起来。字符常量的一个示例是 `'x'`。它可以存储在 `char` 数据类型的变量中。字符常量不必总是像 `'x'` 这样的普通字符，也可以是通用字符（如 `'\u02C0'`）或转义序列（如 `'\t'`）。

### 字符串字面量

这些字面量用双引号括起来，也可以使用 `@"`。字符串常量包含的字符与字符常量可以包含的字符类似。也就是说，它们可以包含转义序列、通用字符以及普通字符。如果需要，可以使用字符串字面量将长行分成多行，各部分之间用空白分隔。

请看以下示例。注意，所有这些形式都是同一个字符串。

```text
"hello, dear"
"hello, " +
"dear"
"hello, " + "dear"
@"hello, dear"
```

现在你已经知道什么是常量，是时候开始定义它们了。需要使用 `const` 关键字来定义常量。常量定义的语法如下。

```csharp
const <data_type> <constant_name> = value;
```

以下示例演示了如何定义常量并在程序中使用它。

```csharp
using System;

namespace DeclaringConstants
{
    class Program
    {
        static void Main(string[] args)
        {
            const double pi = 3.14159;

            // constant declaration

            double r;

            Console.WriteLine("Enter Radius: ");

            r = Convert.ToDouble(Console.ReadLine());

            double areaCircle = pi * r * r;

            Console.WriteLine("Radius: {0}, Area: {1}", r, areaCircle);
            Console.ReadLine();
        }
    }
}
```

编译并执行上述代码后，产生的结果如下。

```text
Enter Radius:
3
Radius: 3, Area: 28.27431
```

### 探索可空类型

C# 中有一种特殊的数据类型，称为可空类型。这些数据类型不仅可以被赋予正常的取值范围，还可以被赋予 null 值。

例如，`Nullable<Int32>` 变量可以取 -2,147,483,648 到 2,147,483,647 范围内的任何值，也可以为 null 值。同样，`Nullable<bool>` 变量可以以 `false`、`true` 或 `null` 作为其值。可空类型声明的语法如下。

```csharp
<data_type> ? <variable_name> = null;
```

以下示例演示了这些数据类型的使用。

```csharp
using System;

namespace CalculatorApplication
{
    class NullablesAtShow
    {
        static void Main(string[] args)
        {
            int? num1 = null;
            int? num2 = 45;
            double? num3 = new double?();
            double? num4 = 3.14157;
            bool? boolval = new bool?();

            // display the values

            Console.WriteLine("Nullables at Show: {0}, {1}, {2}, {3}", num1, num2, num3, num4);

            Console.WriteLine("A Nullable boolean value: {0}", boolval);
            Console.ReadLine();
        }
    }
}
```

编译并执行上述代码后，产生如下结果。

```text
Nullables at Show: , 45, , 3.14157
A Nullable boolean value:
```

### 理解空合并运算符 (??)

这是一种特殊运算符，用于可空引用类型和值类型。只要隐式转换可行，该运算符就可以将一个操作数转换为另一个可空值类型操作数的数据类型。当第一个操作数的值为 null 时，运算符将返回第二个操作数的值；否则，将返回第一个操作数的值。

下面给出的示例应该会让事情更容易理解。

```csharp
using System;

namespace CalculatorApplication
{
    class NullablesAtShow
    {
        static void Main(string[] args)
        {
            double? num1 = null;
            double? num2 = 3.14157;
            double num3;

            num3 = num1 ?? 5.34;
            Console.WriteLine("Value of num3: {0}", num3);

            num3 = num2 ?? 5.34;
            Console.WriteLine("Value of num3: {0}", num3);
            Console.ReadLine();
        }
    }
}
```

如果执行上述代码，将产生以下结果。

```text
Value of num3: 5.34
Value of num3: 3.14157
```

## 第 4 章

### 开始使用 if、else、switch 语句

在计算机编程中，有一些语句无论你使用何种语言，都或多或少保持不变。这种现象是有原因的，因为这些语句是编程中的关键原则。在这里，你将了解其中的三种语句。

- if 语句
- else 语句
- switch 语句

理解这些语句对于学习 C# 或任何其他编程语言都至关重要。

### if、else 语句基础

你会在所有编程语言中找到 'if 语句'，而且它无疑是你将发现的最重要的语句。毕竟，构建条件代码的能力是一项基本


任何软件开发的原则。因此，你需要深入熟悉这一特定的语句。

在C#中，你会发现使用if语句相当简单。事实上，如果你使用过其他编程语言或熟悉它们，你会发现这个特定语句非常容易使用。

关于if语句，你需要知道的最重要的事情之一是它要求一个布尔结果。换句话说，结果必须是true或false。有一些编程语言可以将多种数据类型转换为布尔值，但C#并非如此。在C#中，你必须确保结果被专门制作为布尔类型。一个例子是像`if(number)`这样的语句。这是你不能在C#中使用的。然而，你可以将“number”与某物进行比较，以生成一个布尔结果。

即使你不懂编程，你也应该能够理解else语句的功能。毕竟这是英语的基础。else语句是if语句的伴随者。它的作用是在if语句所声明的条件未被满足时，为代码的执行提供一种替代方案。

### 理解if语句的用法

为了理解if语句和else语句在C#中是如何使用的，一个示例应用程序会很有帮助。因此，这里有一个演示如何在C#中使用条件逻辑的示例。

```
using System;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            int number;

            Console.WriteLine ("Please enter a number between 0 and 10 :");

            number = int.Parse(Console.ReadLine());

            if(number > 10)
                Console.WriteLine ("Hey! The number should be 10 or less!");
            else
```

```
if(number < 0)
    Console.WriteLine ("Hey! The number should be 0 or more!");
    else
    Console.WriteLine ("Good job!");
    Console.ReadLine ();
}
}
}
```

如你所见，这个程序中有两个if语句以及它们伴随的else语句。它们被用于检查用户输入的数字是否在0到10之间。

示例中给出的代码应该很容易理解。首先，系统要求用户输入一个数字。第一个if语句检查该数字是否大于10。如果函数返回true，则向用户显示一条消息，说明该数字应小于10。如果为false，代码继续执行else语句，其下包含第二个if语句。

第二个if语句用于检查用户输入的数字是否小于0。如果为true，则显示一条消息，告诉用户该数字必须大于0。如果为false，程序继续执行伴随的else语句。该语句导致显示“干得漂亮！”消息。

你在本程序中还必须注意的另一件重要事情是，定义条件代码块时缺少{}字符。在C#中，如果代码块只包含一行代码，则不需要{}字符。在你编写自己的代码时，请务必记住这一点。

### switch语句的基础知识

在编程语言中，switch语句类似于一种选择控制机制。它通常用于让变量的值通过多路分支来修改程序执行的控制流。你可以将switch语句视为一组多个if语句。

switch语句将列出一系列可能性，每种可能性都有自己的操作。还会有一个默认操作，当没有其他可能性被返回为true时执行。就像if语句伴随else语句一样，switch语句有一个case语句形式的伴随者。然而，与if else语句不同，必须使用多个case语句搭配一个switch语句。

查看以下代码块以更好地理解switch语句。下面给出的示例包含switch语句最简单的实现之一。

```
int number = 1;

switch (number)
{

case 0:

    Console.WriteLine("The number is zero!");

    break;

case 1:

    Console.WriteLine("The number is one!");

    break;

}
```

如你所见，需要检查的标识符放在switch关键字之后。接着是一系列case语句。这些语句将标识符与特定值进行对比。

你一定注意到了每个case都添加了一个break语句。这是由于编程语言的要求。在C#中，必须在块结束之前离开该块。如果编写的是一个函数，可以用return语句代替break语句。

给定的示例使用了整数。然而，switch语句可以使用任何简单数据类型。此外，多个case语句可以指定相同的操作。

### 理解switch语句的用法

当然，理解switch case语句使用方法的最佳方式是通过示例。以下示例将说明switch语句如何与case语句一起应用。它还突出了switch语句的默认操作功能。

```
Console.WriteLine ("Is C# easy ? (yes/no/maybe)");

string input = Console.ReadLine();

switch (input.ToLower())
{

case "yes":

case "maybe":

    Console.WriteLine ("Awesome!");

    break;
```

然而，用户很有可能会犯下打字错误。用户也可能写下一些不属于给定选项的内容。在这些情况下，如果没有提到default关键字，switch语句将不会产生任何输出。由于此应用程序中使用了它，程序将返回“很抱歉，我不明白那是什么意思！”

default语句的作用是在所有case语句都被证明为false时提供替代操作。当然，这是一个完全可选的语句，但在许多情况下仍然很有用。

你应该已经熟悉这些语句的功能及其使用方式。你现在应该能够轻松地在你的代码中实现if else语句和switch case语句了。

## 第5章

### 用循环在C#中自如穿行

当你在编写软件或应用程序时，你将需要使用循环。这是所有编程语言中普遍存在的一种基本技术。循环可以定义为一系列指令，不断重复，直到某个预定义的条件被满足。简单来说，一个代码块被重复执行一定次数，直到某个条件被满足为止。

通常在一个循环中，会执行某一特定过程。这可以简单到获取特定数据项并修改它。之后，会检查一个条件。例如，可以检查计数器是否已达到特定数字。如果尚未达到该数字，程序的下一指令是返回序列中的第一条指令。这样就重复该序列。一旦条件被满足，该指令将使程序继续执行下一组顺序指令。它也可以从循环中分支出去。

有一种特殊类型的循环称为无限循环。在这种循环中，缺少一个可正常运作的退出指令。结果，循环将不断重复，直到操作系统检测到它，操作系统将终止程序并显示错误。无限循环也可以因某些其他事件的发生而停止。例如，可以让程序在特定时间后自动终止。

在C#中，你会遇到四种不同类型的循环。因此，你需要熟悉它们。

### while循环

C#中四种循环中最简单的是while循环。在这种类型的循环中，只要所定义的条件返回true，一系列指令就会持续执行。只有当条件返回false时它才会退出。以下是一个帮助你理解的示例。

```
using System;

namespace ConsoleApplication1
{

class Program
{

static void Main(string[] args)
{
```



```
int number = 0;
while (number < 10)
{
    Console.WriteLine(number);
    number = number + 1;
}
Console.ReadLine();
}
}
}
```

当你运行这段代码时，你会发现程序在控制台上列出从 0 开始到 10 的数字序列。

当然，变量 number 最初被定义为 0。每次循环执行时，变量都会增加 1。你可以在以下语句中看到这一点：

```
number = number + 1
```

因此，程序会一直显示数字直到达到九，这是最后要显示的内容。你可能会

想知道为什么会显示九，而你在代码中提到了 10。

条件只有在数字小于 10 时才为真。一旦数字变为 10，条件就变为假。毕竟，十不是小于 10。正如你所见，while 循环的条件是在程序进入循环序列之前检查的。一旦数字变为 10，条件就变为假，while 循环序列就不会被执行。

### The do Loop

do 循环与 while 循环有某些相似之处，但有一个主要区别。while 循环在循环序列执行之前检查条件。另一方面，do 循环会在循环执行后检查条件。这意味着循环序列在退出之前至少会执行一次。这在 while 循环中是不可能的。看下面的例子。

```
using System;

namespace ConsoleApplication1
{

class Program
{

static void Main(string[] args)
```

```
{
    int number = 0;
    do
    {
        Console.WriteLine(number);
        number = number + 1;
    } while (number < 10)
    Console.ReadLine();
}
}
```

运行此程序时，你会看到数字从 0 显示到 9。一旦数字变为 10 或超过 10，程序将退出循环序列。正如你所见，do 循环的工作方式与 while 循环类似，但它在序列执行后检查条件。

### The for Loop

for 循环与 do 或 while 循环不同。for 循环通常在你知道想要的确切迭代次数时使用。它也可以在你

定义了一个包含数量的变量时使用。以下示例说明了 for 循环的使用。

```
using System;
namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            int number = 10;
            for (int i = 0; i < number; i++)
                Console.WriteLine(i);
            Console.ReadLine();
        }
    }
}
```

运行此程序时，你会发现输出与前面的示例相同。然而，for 循环

往往比 while 和 do 循环更紧凑，正如你所见。

for 循环有三个部分。首先，为计数初始化一个变量。然后，定义一个条件语句来测试该变量。最后，我们递增计数器变量。在 C# 和其他一些编程语言中，你可以使用 ++ 代替编写整个语句："variable = variable + 1"。结果将是相同的。

第一部分将在实际循环开始之前仅执行一次。这是变量 i 被定义然后设为 0 的部分。接下来的两个部分将在 for 循环的每次迭代中执行。在每次重复中，变量 I 将与 number 变量进行比较。当变量 i 小于 number 变量时，循环将再次运行。执行后，变量 I 将增加 1。在这种情况下，它将继续循环直到变量 I 等于 10。

### The for each Loop

for each 循环与前三个循环大不相同。此循环对一组项目进行操作。数组或其他类型的内置列表类型也可以使用。对于以下示例，使用了 ArrayList，因为它是 C# 中可用的简单列表之一。ArrayList 的工作方式与数组类似。

```
using System;
```

```
using System.Collections;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            ArrayList list = new ArrayList();
            list.Add("Dog");
            list.Add("Cat");
            list.Add("Bird");
            foreach (string name in list)
                Console.WriteLine(name);
            Console.ReadLine();
        }
    }
}
```

正如你所见，代码中首先创建了一个 ArrayList 的实例。随后向列表添加了一些字符串项。在此示例中，我们将一些动物名称作为字符串项添加到 ArrayList list 中。

然后使用 foreach 循环遍历每个项目。在每次重复中，name 变量被设置为在 ArrayList 中到达的项目。然后将此变量推送输出。因此，你可以看到插入到 ArrayList 中的动物在控制台上显示

你必须告知 foreach 循环你希望从集合中取出哪种数据类型。在这种情况下，我们指定 name 变量将属于 string 数据类型。可能你有一个包含不同数据类型的列表。在这种情况下，你可以使用 object 类而不是特定类，以便将列表中的每个项目作为对象取出。

如果你要在程序中使用集合，你会发现 foreach 循环是 C# 中所有循环类型中最好的选择。这主要是因为在这种操作中，foreach 比所有其他循环都简单。

## Chapter 6

### Get Introduced To Encapsulation

面向对象编程中有四个基本概念。它们是继承、抽象、多态性和封装。因此，你在 C# 编程时一定会遇到封装。所以，让我们现在学习它，以便你在选择进阶课程时变得更容易。

封装可以解释为一个或多个项目可以被封闭在物理或逻辑包中的过程。在 OOP 方法中，封装可以防止访问实现细节。

在面向对象编程中，封装和抽象是相关的特性。通过抽象，可以使相关信息可见。另一方面，封装将允许用户在期望的级别实现抽象。

访问说明符用于实现封装。访问说明符将定义类成员的范围和可见性。在 C# 中，将提供对给定访问说明符的支持。

- Public
- Protected
- Private
- Internal
- Protected internal

我们将依次查看这些访问说明符。

### Public Access Specifier

此说明符将允许类向其他函数以及对象公开成员函数和成员变量。可以从其类的外部访问任何公共成员。

看下面的示例以更好地掌握公共访问说明符。

```
using System;

namespace RectangleApplication
{

```

```
class Rectangle
{
    //member variables
    public double length;
    public double width;
    public double GetArea()
    {
        return length * width;
    }
    public void Display()
    {
        Console.WriteLine("Length: {0}", length);
        Console.WriteLine("Width: {0}", width);
        Console.WriteLine("Area: {0}", GetArea());
    }
}//end class Rectangle
class ExecuteRectangle
{
```

```
static void Main(string[] args)
{
    Rectangle r = new Rectangle();
    r.length = 4.5;
    r.width = 3.5;
    r.Display();
    Console.ReadLine();
}
}
}
```

执行上面显示的代码后将产生以下结果。

Length: 4.5

Width: 3.5

Area: 15.75

在上面的示例中，注意成员变量 width 和 length 被声明为 public。因此，可以通过 Rectangle 类的实例 r 从函数 Main() 访问它们。此外，成员函数，


GetArea() 和 Display() 也可以直接访问这些变量，而无需使用类的任何实例。成员函数 Display() 也被声明为 public。这样，它也可以从 Main() 中通过 Rectangle 类的实例 r 进行访问。

### 私有访问修饰符

使用此修饰符，类可以对其对象和函数隐藏成员函数和成员变量。只有属于同一类的函数才能访问私有成员。甚至类的实例也无法访问私有成员。

下面的示例说明了私有访问修饰符的概念。

```
using System;

namespace RectangleApplication
{

class Rectangle
{

//member variables

private double length;

private double width;
```

```
Length: 4.4
Width: 3.3
Area: 14.52
```

在上面的示例中，您会注意到成员变量 width 和 length 已被声明为 private。因此，无法从 Main() 函数访问它们。只有成员函数 Display() 和 AcceptDetails() 可以访问这些变量。由于这些成员函数已声明为 public，因此可以从 Main() 中使用 Rectangle 类的实例 r 访问它们。

### 受保护访问修饰符

此修饰符将使子类能够访问基类的成员函数和成员变量。因此，该修饰符在实现继承时非常有用。

### 内部访问修饰符

此修饰符将允许类在当前程序集中向其他对象和函数公开其成员函数和成员变量。也就是说，带有内部访问修饰符的成员可以从该成员所在应用程序中定义的任何方法或类访问。

查看以下示例以更好地理解此修饰符。

```
using System;

namespace RectangleApplication
{
    class Rectangle
    {
        //member variables
        internal double length;
        internal double width;
        double GetArea()
        {
            return length * width;
        }
        public void Display()
        {
            Console.WriteLine("Length: {0}", length);
            Console.WriteLine("Width: {0}", width);
            Console.WriteLine("Area: {0}", GetArea());
        }
    }//end class Rectangle

    class ExecuteRectangle
    {
        static void Main(string[] args)
        {
            Rectangle r = new Rectangle();
            r.length = 4.5;
            r.width = 3.5;
            r.Display();
            Console.ReadLine();
        }
    }
}
```

执行上述代码后，会得到以下结果。

```
Length: 4.5
Width: 3.5
Area: 15.75
```

您会注意到在示例中，GetArea() 未使用任何访问修饰符声明。如果未指定访问修饰符，类成员将获得默认的私有访问修饰符。

### 受保护内部访问修饰符

此访问修饰符允许类将其成员函数和成员变量对其他类函数和对象隐藏。只有同一应用程序中的子类（如果有）才能访问这些成员。此访问修饰符通常用于实现继承。

## 第7章：认识 C# 中的类及其属性

您还记得，C# 是一种面向对象的编程语言。如果您对计算机编程有所了解，那么您一定听说过类。类在面向对象编程中至关重要。

可以说，类是一种构造，通过将不同类型的变量、事件和方法组合在一起，您可以构建自定义类型。换句话说，类是一个包含相互关联的变量和方法的集合。类将描述这些内容。在大多数情况下，您将创建类的实例，该实例被称为对象。您可以在此对象上使用已定义的变量和方法。当然，您可以根据代码的需求创建类的多个实例。

### 理解类

在之前的示例中，您已经接触过类的使用。毕竟，您在 C# 中构建的任何内容都必须以类为基础。通过以下示例可以获得更好的理解。

```
using System;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            Car car;
            car = new Car("Red");
            Console.WriteLine(car.Describe());
            car = new Car("Green");
            Console.WriteLine(car.Describe());
            Console.ReadLine();
        }
    }
}

class Car
{
    private string color;
    public Car(string color)
    {
        this.color = color;
    }
    public string Describe()
    {
        return "This car is " + Color;
    }
    public string Color
    {
        get { return color; }
        set { color = value; }
    }
}
```

正如您所见，首先定义了一个新类，并将其命名为 Car。为了简便起见，该类与主应用程序一起在同一个文件中声明。通常，新类倾向于定义在它们自己的文件中，但是，

还定义了一个变量，名为 color。此外，它被声明为私有变量。这是您应该记住的一点。通常应使用属性从外部访问变量。在 Car 类的末尾，定义了 Color 属性。这允许访问 color 变量。

Car 类还定义了一个构造函数，该构造函数接收一个参数。这允许我们使用颜色来初始化 Car 对象。由于此应用程序中只有一个构造函数，因此只能使用颜色来实例化 Car 对象。

还使用了 Describe() 方法。其目的是让用户在获取已记录信息的同时获得一些额外文本。它只会返回一个字符串以及已提供的数据。

在主应用程序中，声明了一个类型为 Car 的变量。随后创建了一个新实例，参数为“Red”。根据类的编码方式，红色将被分配为汽车的颜色。

为了验证这一点，再次使用了 Describe() 方法。

再次执行相同的步骤，以向您展示创建同一个类的多个实例实际上非常容易。当然，这一次使用了另一种颜色。

### 理解类的属性

属性的作用是让您能够控制类变量的可访问性。在任何面向对象的编程语言中，属性始终是从外部访问变量的推荐方式。在之前的示例中，您已经接触过属性的使用。

可以说，属性是方法和变量的组合。因此，它不能接受任何参数。另一方面，值可以在返回之前进行处理。属性将由两个部分组成。会有 get 方法和 set 方法。两者将一起包含在属性中。您可以在以下代码中看到这样的示例。

```
private string color;
public string Color
{
    get { return color; }
    set { color = value; }
}
```

get 方法必须用于返回变量。另一方面，set 方法必须用于为该变量赋值。当然，上面的示例是一个涉及属性的非常简单的代码示例。因此，完全有可能进一步扩展它。

关于属性，还有一点您应该了解。一个属性至少需要一个方法才能工作。换句话说，您可以使用 get 方法或 set 方法。在这种情况下，另一个方法变为可选。这种技术允许您根据需求定义只读属性或只写属性。

这里是另一个示例，进一步说明了属性的潜力。

```
public string Color
{
    get
    {
        return color.ToUpper();
    }
}
```



}
set
{
    if (value == "Red")
        color = value;
    else
        Console.WriteLine("This car can only be red!");
}
正如你所见，这是一段更复杂的代码，包含更高级的属性。现在，你会发现 color 变量在返回时只会以大写字符形式出现。这是因为在返回之前对变量添加了 ToUpper() 方法。代码的下一部分将设置 color 变量。然而，唯一会被接受的值是“Red”。

### A Short Guide to Visibility

在阅读本指南的过程中，你会遇到 public 和 private 这两个术语。你可能在想它们代表什么。嗯，它们是表示所讨论项可见性的关键字。

protected internal 项的类即使继承类存在于另一个项目中也可以访问该项。

你现在应该能够自行创建简单的类，甚至创建它们的属性。当然，这只是基础水平。通过练习和进一步的知识，你可以创建功能强大且令人惊叹的程序，其中包含多个类和属性。

### Getting a Grip on Member Functions and Encapsulation

在类中，成员函数是一个其原型或定义在类定义内、方式与其它变量类似的函数。成员函数可以操作其类的任何对象。它还可以访问该对象类的每个成员。

另一方面，成员变量是对象的属性。因此，它们将被保持为私有以实现封装。它们只能通过使用公共成员函数来访问。

以下示例说明了类成员的使用。在这里，正在查找不同类成员的值。

```
using System;
```
```
namespace BoxApplication
```
```
{
```
```
class Box
{
    private double length; // Length of a box
    private double breadth; // Breadth of a box
    private double height; // Height of a box
    public void setLength( double len )
    {
        length = len;
    }
    public void setBreadth( double bre )
    {
        breadth = bre;
    }
    public void setHeight( double hei )
    {
        height = hei;
    }
    public double getVolume()
```
```
Box2.setBreadth(13.0);
Box2.setHeight(10.0);
// volume of box 1
volume = Box1.getVolume();
Console.WriteLine("Volume of Box1 :{0}",volume);
// volume of box 2
volume = Box2.getVolume();
Console.WriteLine("Volume of Box2 :{0}",volume);
Console.ReadKey();
}
}
}
```

执行上面给出的代码后，将会产生以下结果。

Volume of Box1 :210

Volume of Box2 :1560

### Static Members of a Class in C#

类成员可以用 static 关键字定义为静态。在将类的特定成员声明为静态时，

无论为该类创建了多少个对象，该静态成员都只有一个副本。

换句话说，static 关键字表示对于一个类，该成员只有一个实例存在。静态变量倾向于用于定义常量。这是因为可以通过调用类而无需创建实例来检索它们的值。静态变量的初始化可以在类定义或成员函数之外进行。同时，静态变量也可以在类定义内部初始化。

看下面的例子。

```
using System;

namespace StaticVarApplication
{
    class StaticVar
    {
        public static int num;
        public void count()
        {
            num++;
```
```
}

public int getNum()
{
    return num;
}

}

class StaticTester
{
    static void Main(string[] args)
    {
        StaticVar s1 = new StaticVar();
        StaticVar s2 = new StaticVar();

        s1.count();
        s1.count();
        s1.count();

        s2.count();
        s2.count();
        s2.count();
    }
}
```
```
```
```
Console.WriteLine("Variable num for s1: {0}",
s1.getNum());
Console.WriteLine("Variable num for s2: {0}",
s2.getNum());
Console.ReadKey();
}
}
}
```
```

执行上面所示的代码时，会产生以下结果。

Variable num for s1: 6

Variable num for s2: 6

成员函数也可以声明为静态。这些函数将只访问静态变量。此外，静态函数甚至可以在创建对象之前存在。

看下面的例子以更好地理解这些静态函数。

```
```csharp
using System;
namespace StaticVarApplication
{
```
```
class StaticVar
{
public static int num;
public void count()
{
num++;
}
public static int getNum()
{
return num;
}
}

class StaticTester
{
static void Main(String[] args)
{
StaticVar s = new StaticVar();
s.count();
}
}
```
```
s.count();

s.count();

Console.WriteLine("Variable    num:    {0}", StaticVar.getNum());

Console.ReadKey();
}
}
}
```

编译并执行上面的代码后，你会发现产生以下结果。

Variable num: 3

## Chapter 8

### A Brief on Methods

在阅读本书时，你会多次遇到方法。如果你想知道它们是什么，那么这里就是你了解它们的地方。方法是关于编程的基础知识之一，你应该知道。

### What is a Method?

方法可以说是一组可以一起执行任务的语句。所有 C# 程序至少会有一个类，其中包含一个名为 Main 的方法。你已经遇到过它们。

为了使用方法，必须先定义该方法。然后，调用该方法。让我们逐一看看这个过程。

### Defining a Method

当方法被定义时，方法结构的各个元素会被声明。在 C# 语言中定义方法的语法如下所示。

```
<Access Specifier> <Return Type> <Method Name>(Parameter List)
```
```
{
```
```
Method Body
```
```
}
```

方法可以有各种元素。它们如下所述。

Access Specifier: 正如你所知，访问说明符将决定方法或变量从另一个类中的可见性。

Return Type: 方法可能返回值。返回类型说明了方法将返回的值的数据类型。如果方法没有返回值，则返回类型为 void。

Method name: 这是方法的唯一标识符。名称区分大小写。此外，标识符不能与类中已声明的任何其他标识符相同。

Parameter list: 参数用于在方法之间传递和接收数据。它们用括号括起来。参数列表将指明方法的参数的顺序、数量和类型。重要的是，方法可能没有任何参数。

Method Body: 主体将包含完成活动所需的指令集。

看下面给出的示例。在这段代码片段中，你会注意到一个函数 FindMax。它接受两个整数值并比较它们。较大的值将被返回。该函数具有 public 访问说明符。因此，它可以通过使用其实例从类外部访问。

```
class NumberManipulator
{
    public int FindMax(int num1, int num2)
    {
        /* local variable declaration */
        int result;
        if (num1 > num2)
            result = num1;
        else
```
```
result = num2;

return result;
}
...
}
```

### Calling a Method

在 C# 中，调用方法非常容易，只需使用其名称即可。看下面给出的示例。它展示了如何调用方法。

```
using System;

namespace CalculatorApplication
{

class NumberManipulator
{

public int FindMax(int num1, int num2)
{

/* local variable declaration */

int result;

if (num1 > num2)
```





```
result = num1;
else
result = num2;
return result;
}

static void Main(string[] args)
{
/* local variable definition */
int a = 100;
int b = 200;
int ret;
NumberManipulator n = new NumberManipulator();
//calling the FindMax method
ret = n.FindMax(a, b);
Console.WriteLine("Max value is : {0}", ret);
Console.ReadLine();
}
}
```

执行上述代码后，将产生以下结果。

Max value is : 200

只需使用方法所属类的实例，就可以从其他类调用公共方法。下面的示例演示了具体做法。在此例中，FindMax 方法是 NumberManipulator 类的一部分。它可以从另一个名为 Test 的类中调用。

```
using System;

namespace CalculatorApplication
{
    class NumberManipulator
    {
        public int FindMax(int num1, int num2)
        {
            /* local variable declaration */
            int result;

            if(num1 > num2)
```
```
result = num1;
else
result = num2;
return result;
}
}
class Test
{
static void Main(string[] args)
{
/* local variable definition */
int a = 100;
int b = 200;
int ret;
NumberManipulator n = new NumberManipulator();

/* calling the FindMax method */
ret = n.FindMax(a, b);

Console.WriteLine("Max value is : {0}", ret);
}
}
```
```
Console.ReadLine();
}
}
}
```

上述示例将产生如下结果。

Max value is : 200

### 理解递归方法调用

方法可以调用自身，这样的过程称为递归。下面的示例说明了递归方法调用的用法。这里，借助递归方法调用计算给定数字的阶乘。

```
using System;
```
```
namespace CalculatorApplication
```
```
{
```
```
class NumberManipulator
```
```
{
```
```
public int factorial(int num)
```
```
{
```
```
/* local variable declaration */
```
```
int result;

if(num == 1)
{
    return 1;
}
else
{
    result = factorial(num - 1) * num;
    return result;
}
}

static void Main(string[] args)
{
    NumberManipulator n = new NumberManipulator();
    //calling the factorial method
    Console.WriteLine("Factorial of 6 is : {0}", n.factorial(6));
    Console.WriteLine("Factorial of 7 is : {0}", n.factorial(7));
```
```
Console.WriteLine("Factorial of 8 is : {0}", n.factorial(8));
Console.ReadLine();
}
}
}
```

编译并执行上述代码后，将产生以下结果。

Factorial of 6 is : 720
Factorial of 7 is : 5040
Factorial of 8 is : 40320

### 如何向方法传递参数？

如果调用的方法带有参数，则必须将参数传递给该方法。有三种方式可以向方法传递参数。我们将逐一介绍。

按值传递参数是向方法传递参数时的默认机制。在这种情况下，当方法被调用时，会为每个值参数创建一个新的存储位置。然后，原始参数的值会被复制到这些新位置中。方法内部对参数所做的任何更改都不会影响实参。

请看下面的示例。

```
using System;

namespace CalculatorApplication
{
    class NumberManipulator
    {
        public void swap(int x, int y)
        {
            int temp;

            temp = x; /* save the value of x */
            x = y;   /* put y into x */
            y = temp; /* put temp into y */
        }
        static void Main(string[] args)
        {
```
```
NumberManipulator n = new NumberManipulator();
/* local variable definition */
int a = 100;
int b = 200;
Console.WriteLine("Before swap, value of a : {0}", a);
Console.WriteLine("Before swap, value of b : {0}", b);
/* calling a function to swap the values */
n.swap(a, b);
Console.WriteLine("After swap, value of a : {0}", a);
Console.WriteLine("After swap, value of b : {0}", b);
Console.ReadLine();
}
}
}
```

执行上述代码的结果如下。

Before swap, value of a :100

Before swap, value of b :200

After swap, value of a :100

After swap, value of b :200

### 引用参数

这是对变量内存位置的引用。使用这种机制时，不会像值参数那样为参数创建新的存储位置。引用参数将表示提供给方法的实际参数的确切内存位置。可以借助 ref 关键字声明引用参数。

请看下面的示例。

```
using System;

namespace CalculatorApplication
{
    class NumberManipulator
    {
        public void swap(ref int x, ref int y)
        {
            int temp;
            temp = x; /* save the value of x */
            x = y;  /* put y into x */
```
```
y = temp; /* put temp into y */
}

static void Main(string[] args)
{
    NumberManipulator n = new NumberManipulator();
    /* local variable definition */
    int a = 100;
    int b = 200;
    Console.WriteLine("Before swap, value of a : {0}", a);
    Console.WriteLine("Before swap, value of b : {0}", b);
    /* calling a function to swap the values */
    n.swap(ref a, ref b);
    Console.WriteLine("After swap, value of a : {0}", a);
    Console.WriteLine("After swap, value of b : {0}", b);
    Console.ReadLine();
}
}
```
```
}
```

执行上述代码后，将产生以下结果。

Before swap, value of a : 100

Before swap, value of b : 200

After swap, value of a : 200

After swap, value of b : 100

正如您所看到的，swap 函数中的值已被更改。这种更改也会反映在 Main 函数中。

### 输出参数

return 语句只能从函数中返回一个值。尽管如此，借助输出参数，函数可以返回两个值。事实上，输出参数与引用参数非常相似。然而，二者有一个主要区别：输出参数能够将数据从给定方法中传出，而不是传入。

下面的示例演示了输出参数的用法。

```
using System;
```
```
namespace CalculatorApplication
```
```
{
```
```
class NumberManipulator
{
    public void getValue(out int x)
    {
        int temp = 5;
        x = temp;
    }
    static void Main(string[] args)
    {
        NumberManipulator n = new NumberManipulator();
        /* local variable definition */
        int a = 100;
        Console.WriteLine("Before method call, value of a : {0}", a);
        /* calling a function to get the value */
        n.getValue(out a);
        Console.WriteLine("After method call, value of a : {0}", a);
    }
```
```
Console.ReadLine();
}
}
}
```

执行上述示例中的代码后，将产生以下结果。

Before method call, value of a : 100

After method call, value of a : 5

对于输出参数，提供的变量不需要为其赋值。因此，当您必须通过参数从方法中返回值，而又不想为参数赋予初始值时，输出参数非常有用。

下面的示例对此进行了演示。

```
using System;

namespace CalculatorApplication
{

class NumberManipulator
{
```
```
public void getValues(out int x, out int y)
{
    Console.WriteLine("Enter the first value: ");
    x = Convert.ToInt32(Console.ReadLine());
    Console.WriteLine("Enter the second value: ");
    y = Convert.ToInt32(Console.ReadLine());
}

static void Main(string[] args)
{
    NumberManipulator n = new NumberManipulator();
    /* local variable definition */
    int a , b;
    /* calling a function to get the values */
    n.getValues(out a, out b);
    Console.WriteLine("After method call, value of a : {0}", a);
    Console.WriteLine("After method call, value of b : {0}", b);
    Console.ReadLine();
}
```



}
}

执行上述示例后，您将得到以下结果。

Enter the first value:

7

Enter the second value:

8

After method call, value of a : 7

After method call, value of b : 8

相反，我们创建一个数组 a，并使用 a[0]、a[1] 和 a[2] 等。

请记住，数组中的特定元素可以通过索引访问。在 C# 中，所有数组都拥有连续的内存位置。最低地址对应于数组的第一个元素，而最高地址属于最后一个元素。

### 声明数组

在 C# 中，如果要声明数组，必须使用以下语法。

```
datatype[] arrayName;
```

该语法的各个组成部分讨论如下。

- datatype 用于指定数组中元素的类型。
- [] 指定数组的秩。数组的秩定义数组的大小。
- arrayName 是该数组的名称。

### 初始化数组

请记住，声明数组不会在内存中初始化它。只有初始化数组变量后，才能为其赋值。由于数组是引用类型，您必须使用 new 关键字来创建给定数组的实例。

下面的示例说明了具体做法。

```
double[] balance = new double[10];
```

### 给数组赋值

可以给数组的各个元素赋值。为此，需要使用元素的索引号。下面的示例说明了这一点。

```
double[] balance = new double[10];
```

```
balance[0] = 4500.0;
```

也可以在声明数组时为其赋值。

```
double[] balance = { 2340.0, 4523.69, 3421.0 };
```

还可以同时创建和初始化数组。

```
int [] marks = new int[5] { 99, 98, 92, 97, 95 };
```

如果需要，可以省略数组的大小。

```
int [] marks = new int[] { 99, 98, 92, 97, 95 };
```

数组变量可以被复制到另一个数组变量。在这种情况下，目标数组变量以及源数组变量都将

```csharp
{
static void Main(string[] args)
{
	int [] n = new int[10]; /* n is an array of 10 integers */
	int i,j;
	/* initialize elements of array n */
	for (i = 0; i < 10; i++)
	{
		n[i] = i + 100;
	}
	 /* output each array element's value */
	for (j = 0; j < 10; j++)
	{
		Console.WriteLine("Element[{0}] = {1}",j, n[j]);
	}
	Console.ReadKey();
}
}
```

执行上述代码后，将产生以下结果。

Element[0] = 100

Element[1] = 101

Element[2] = 102

Element[3] = 103

Element[4] = 104

Element[5] = 105

Element[6] = 106

Element[7] = 107

Element[8] = 108

Element[9] = 109

### C# 中与数组相关的概念

在 C# 中处理数组时，有几个重要概念需要了解。它们在高级课程中可能会很有用。

### 多维数组

C# 支持多维数组。这些数组最常见和最简单的形式是二维数组。

### 交错数组

简单来说，这些数组就是数组的数组。

### Array 类

该类定义在 System 命名空间中。它是所有数组的基类。因此，它提供了许多方法和属性，以便在操作数组时为您提供帮助。

### 将数组传递给函数

可以将数组传递给函数。这可以通过指定数组的名称（不带索引）来实现。

### 参数数组

它们用于向给定函数传递数量不定的参数。

关于数组的部分到此结束。接下来，我们将研究字符串。

### 字符串简介

在 C# 中，字符串可以用作字符数组。尽管如此，常见做法是使用 string 关键字来声明存储变量。您必须记住，string 关键字只是 System.String 类的别名。

### 创建字符串对象

可以通过以下任一过程创建字符串对象。

- 通过将字符串字面量赋值给 String 变量
- 使用 String 类构造函数
- 通过检索属性或调用可返回字符串的方法
- 通过使用字符串连接运算符 +
- 通过调用格式化方法，将对象或值转换为相应的字符串表示形式

下面的示例说明了字符串对象的创建。

```
using System;

namespace StringApplication
{
    class Program
    {
        static void Main(string[] args)
        {
```

```csharp
//from string literal and string concatenation
string fname, lname;
fname = "John";
lname = "Smith";
string fullname = fname + lname;
Console.WriteLine("Full Name: {0}", fullname);
```

```csharp
//by using string constructor
char[] letters = { 'H', 'e', 'l', 'l', 'o' };
string greetings = new string(letters);
Console.WriteLine("Greetings: {0}", greetings);
```

```csharp
//methods returning string
string[] sarray = { "Hello", "From", "The", "Earth" };
string message = String.Join(" ", sarray);
Console.WriteLine("Message: {0}", message);
```

```csharp
//formatting method to convert a value
DateTime waiting = new DateTime(2016, 10, 17, 58, 1);
string chat = String.Format("Message sent at {0:t} on {0:D}", waiting);
```

```csharp
Console.WriteLine("Message: {0}", chat);
}
}
}
```

编译并执行上述代码后，将产生以下结果。

```
Full Name: Rowan Atkinson
Greetings: Hello
Message: Hello From The Earth
Message: Message sent at 5:58 PM on Wednesday, October 10, 2016
```

### String 类属性

String 类拥有两个属性。如下所列。

- Chars：获取给定 String 对象中指定位置的 Char 对象。
- Length：获取给定 String 对象中的字符总数。

### String 类中的方法

String 类中有多个可用方法。在处理字符串对象时，这些方法会很有帮助。以下是一些常用的方法。

### public static int Compare(string strA, string strB)

比较两个给定的字符串对象。返回一个整数，指示这两个对象在排序顺序中的相对位置。

### public static int Compare(string strA, string strB, bool ignoreCase )

比较两个给定的字符串对象，并返回一个整数，指示这两个对象在排序顺序中的相对位置。但是，当布尔参数为 true 时，它将忽略大小写。

### public static string Concat(string stro, string str1)

连接两个字符串对象。可以增加要连接的字符串对象的数量。

### public bool Contains(string value)

返回一个值，指示给定的 String 对象是否存在于给定字符串中。

### public static string Copy(string str)

创建一个与给定字符串具有相同值的新 String 对象。

### public bool EndsWith(string value)

确定给定字符串对象的结尾是否与给定字符串匹配。

### public static bool Equals(string a, string b)

确定两个给定的 String 对象是否具有完全相同的值。

### public int IndexOf(char value)

返回给定 Unicode 字符在字符串中的索引。将提供该字符首次出现的从零开始的索引。

### public static string Format(string format, Object argo)

替换给定字符串中的一个或多个格式项。它们将被替换为给定对象的字符串表示形式。

### public string Insert(int startIndex, string value)

返回一个新字符串，该字符串在给定字符串对象中的特定索引位置插入了给定字符串。





### public static bool IsNullOrEmpty(string value)

这表示给定的字符串是否为空字符串或空字符串。

### public static string Join(string separator, params string[] value)

这将使用给定的分隔符连接字符串数组中的所有元素，并在其中每个元素之间使用该分隔符。

### public static string Join(string separator, string[] value, int startIndex, int count)

这将使用给定的分隔符连接字符串的指定元素，并在每个元素之间使用该分隔符。

### public int LastIndexOf(char value)

这返回给定 Unicode 字符在当前字符串对象内部的索引位置。 将使用基于零的索引位置，并且只会提及最后一次出现。

### public string Remove(int startIndex)

这将从指定位置开始删除当前实例中存在的所有字符。 它将一直持续到最后位置。 最后，将返回字符串。

String 类还有其他各种方法和构造函数。 MSDN 库包含完整的列表。 现在，

让我们看一下几个示例，演示如何使用上面给出的某些方法。

下面的示例说明了如何比较字符串。

```
using System;

namespace StringApplication
{
    class StringProg
    {
        static void Main(string[] args)
        {
            string str1 = "This is test";
            string str2 = "This is text";
            if(String.Compare(str1, str2) == 0)
            {
                Console.WriteLine(str1 + " and " + str2 + " are equal.");
            }
            else
            {

```
```
Console.WriteLine(str1 + " and " + str2 + " are not equal.");
}

Console.ReadKey();
}
}
}
```

执行上面显示的代码后，将产生以下结果。

This is a test, and This is text are not equal.

下面显示的示例演示了一个包含另一个字符串的字符串。

```
using System;

namespace StringApplication
{
    class StringProg
    {
        static void Main(string[] args)
        {
```

```
string str = "This is test";
if (str.Contains("test"))
{
    Console.WriteLine("The sequence 'test' was found.");
}
Console.ReadKey();
}
}
}
```

执行上面显示的代码后会产生以下结果。

The sequence 'test' was found.

下面给出了示例，说明如何获取子字符串。

```
using System;
namespace StringApplication
{
class StringProg
{
```

```
static void Main(string[] args)
{
    string str = "Last night I dreamt of San Pedro";
    Console.WriteLine(str);
    string substr = str.Substring(23);
    Console.WriteLine(substr);
}
}
}
```

编译并执行上述代码时，会产生以下结果：

San Pedro

### Joining Strings:

```
using System;

namespace StringApplication
{
    class StringProg
    {
```

```
static void Main(string[] args)
{
    string[] starray = new string[]{"Down the way nights are dark",
    "And the sun shines daily on the mountain top",
    "I took a trip on a sailing ship",
    "And when I reached Jamaica",
    "I made a stop"};
    string str = String.Join("\n", starray);
    Console.WriteLine(str);
}
}
}
```

执行上面显示的代码后产生的结果如下所示。

Down the way nights are dark
And the sun shines daily on the mountain top
I took a trip on a sailing ship

And when I reached Jamaica

I made a stop

至此，我们已经结束了数组和字符串的介绍。 这里提供的信息对于大多数 C# 初学者级别的项目来说应该足够了。

## Chapter 10

### An Insight to Structures and Enums

现在你已经了解了数组和字符串，是时候了解一下结构和枚举了。 它们在各种程序中发挥着重要作用。 因此，让我们进一步了解它们。

### What is a Structure?

C# 中的结构是值类型数据类型。 有了它，单个变量就可以保存不同数据类型的相关数据。 要创建结构，您必须使用 struct 关键字。 结构通常用于表示记录。

让我们以图书馆书籍为例更好地理解结构。 在图书馆里，你必须跟踪书籍。 现在，在跟踪每本书时，您可能想要考虑的各种属性，例如标题、作者和主题等。 我们将在以下各节的程序中使用此示例。

```
public string author;
public string subject;
public int book_id;
};
public class testStructure
{
public static void Main(string[] args)
{
Books Book1; /* Declare Book1 of type Book */
Books Book2; /* Declare Book2 of type Book */
/* book 1 specification */
Book1.title = "C# Programming";
Book1.author = "John Smith";
Book1.subject = "C# Programming Tutorial";
Book1.book_id = 123456;
/* book 2 specification */
Book2.title = "Java Programming";
Book2.author = "Jane Smith";
```

```
Book2.subject = "Java Programming Tutorial";
Book2.book_id = 456789;
/* print Book1 info */
Console.WriteLine("Book 1 title : {0}", Book1.title);
Console.WriteLine("Book 1 author : {0}", Book1.author);
Console.WriteLine("Book 1 subject : {0}", Book1.subject);
Console.WriteLine("Book 1 book_id :{0}", Book1.book_id);
/* print Book2 info */
Console.WriteLine("Book 2 title : {0}", Book2.title);
Console.WriteLine("Book 2 author : {0}", Book2.author);
Console.WriteLine("Book 2 subject : {0}", Book2.subject);
Console.WriteLine("Book 2 book_id : {0}", Book2.book_id);
Console.ReadKey();
}
}
```

编译并执行上面显示的代码后，将产生以下结果。

Book 1 title : C# Programming

- 结构与类不同，不能从其他结构或类继承。
- 同样，不可能将它们用作其他类或结构的基类。
- 您不能将结构成员指定为 virtual、abstract 或 protected。
- 结构可以实现一个或多个接口。
- 使用 New 运算符创建 struct 对象时，它将被创建并调用正确的构造函数。 与类不同，struct 对象可以在不使用 New 运算符的情况下实例化。
- 如果您不使用 New 运算符，字段将保持未分配状态。 结果是，直到您初始化所有字段，对象将无法使用。

### The Difference between Classes and Structures

这两者之间有几点不同。 它们如下所示。

- 结构是值类型，而类是引用类型。
- 与类不同，结构不支持继承。

- 结构不能有默认构造函数。

现在我们对结构有了更多的了解，让我们重新创建之前的 Books 结构示例，以便更好地理解。

```
using System;

struct Books
{
    private string title;
    private string author;
    private string subject;
    private int book_id;
    public void getValues(string t, string a, string s, int id)
    {
        title = t;
        author = a;
        subject = s;
        book_id = id;
    }
}
```

```
```csharp
public void display()
{
    Console.WriteLine("Title : {0}", title);
    Console.WriteLine("Author : {0}", author);
    Console.WriteLine("Subject : {0}", subject);
    Console.WriteLine("Book_id : {0}", book_id);
}
};

public class testStructure
{
    public static void Main(string[] args)
    {
        Books Book1 = new Books();  /* Declare Book1 of type Book */
        Books Book2 = new Books();  /* Declare Book2 of type Book */

        /* book 1 specification */
        Book1.getValues("C# Programming",
```

```
"John Smith", "C# Programming Tutorial",123456);
/* book 2 specification */
Book2.getValues("Java Programming",
"Jane Smith", "Java Programming Tutorial", 456789);
/* print Book1 info */
Book1.display();
/* print Book2 info */
Book2.display();
Console.ReadKey();
}
}
```

执行上面的代码后，结果将与下面所示相同。

Title : C# Programming

Author : John Smith

Subject : C# Programming Tutorial

Book_id : 123456

Title : Java Programming





Author : Jane Smith

Subject : Java Programming Tutorial

Book_id : 456789

With that, the section on structures comes to an end. Now, let us take a look at enums.

### What is Enums?

Enums are short for enumerations. An enumeration can be said to be a set of named integer constants. The enum keyword is used for declaring an enumerated type. In C#, enumerations are of the value datatype. As such, an enumeration will contain its own values. It is incapable of inheriting or passing inheritance.

### Declaring an enum Variable

Generally, the syntax you need to follow to declare an enumeration is given below.

```
enum <enum_name>
{
    enumeration list
};
```

Take a look at what each of these elements means.

- **enum_name:** This specifies the name of the enumeration type.
- **enumeration list:** This is a list of identifiers, each of which is separated by commas.

In the enumeration list, each symbol represents an integer value. Each symbol will be greater than the one preceding it. The default value of the first symbol in an enumeration list will be 0.

The following example illustrates the use of enumeration variables.

```
using System;

namespace EnumApplication
{

class EnumProgram
{

enum Days { Sun, Mon, Tue, Wed, Thu, Fri, Sat };

static void Main(string[] args)
{

int WeekdayStart = (int)Days.Mon;

int WeekdayEnd = (int)Days.Fri;

Console.WriteLine("Monday: {0}", WeekdayStart);

Console.WriteLine("Friday: {0}", WeekdayEnd);
```

## Chapter 11

### Becoming Familiar with the Concept of Inheritance

As mentioned in the previous chapter, one of the most important aspects of any object oriented programming language is classes. In the same way, inheritance is a key concept in object oriented programming.

As C# is such a language, you will have to utilize inheritance sooner than later. In fact, the entirety of the .NET framework has been built upon the concept of inheritance. It is responsible for the expression that everything is an object.

Inheritance, in simple terms, enables you to create classes that can inherit specific attributes from their parent classes. In C#, even a simple number can be an instance of a class that inherits from the parent class, System.Object.

Inheritance can be a bit advanced for some beginners. However, it is better to become familiar with it sooner than later because of the roles it plays in C# programming. Here is an example that illustrates the use of inheritance.

```
public class Animal
{
    public void Greet()
    {
        Console.WriteLine("Hello! I’m some kind of animal.");
    }
}

public class Cat: Animal
{
}
```

As you can see, an Animal class has been defined first along with a simple method that sends out a greeting to the user. This is followed up by defining a Cat class. We now use a colon to inform C# that the Cat class is going to be inheriting from the Animal class. Now, it is possible to start using these classes

```
Animal animal = new Animal();

animal.Greet();
```

```
{
    Console.WriteLine ("Hello! I'm a cat.");
}
}
```

As you can notice, there are a few changes to the code in the above examples. A method has been added on the Cat Class and, on the Animal class, the virtual keyword has been added to the method. Additionally, there is the presence of the override keyword on the Cat class.

In C#, it is not possible to override an item of any class unless it has been marked as virtual. It is certainly possible to keep accessing the inherited method even after it has been overridden with the help of the base keyword. This is shown in the example below.

```
public override void Greet()
{
    base.Greet();
    Console.WriteLine ("Yes! I am - a cat!");
}
```

However, methods are not the only thing that can be inherited. In fact, nearly all members of a class will be inherited. This includes properties and fields. All you need to ensure the proper result is to utilize the proper visibility, as explained in the earlier chapter.

Another thing you need to remember is that inheritance need not take place from one class to another. It is possible to have an entire hierarchy of classes that inherit from one another. Keeping in tune with the earlier examples, it is possible to create a Kitten class that inherits from the Cat class and that, in turn, will be inheriting from the Animal class.

However, there is one thing that you cannot perform in C#, and that is multiple inheritances. In other words, you cannot make a class inherit from multiple classes simultaneously. C# does not support this feature.

### Understanding the Concept of Base Class and Derived Class

It is possible for a class to be derived from more than a single class. As a result, it is possible to inherit the functions and data from multiple base classes.

Given below is the syntax used to create derived classes in C#.

```
```csharp
<access-specifier> class <base_class>

{

...
```
```

```
}
class <derived_class> : <base_class>
{
...
}
```

Let us take the help of an example to get a better understanding of base classes and derived classes. In the following example, Shape is the base class while Rectangle is its derived class.

```
using System;

namespace InheritanceApplication
{

class Shape
{

public void setWidth(int w)
{

width = w;

}

public void setHeight(int h)
```

```
{
    height = h;
}
protected int width;
protected int height;
}
// Derived class
class Rectangle: Shape
{
    public int getArea()
    {
        return (width * height);
    }
}
class RectangleTester
{
    static void Main(string[] args)
```

```
{
    Rectangle Rect = new Rectangle();
    Rect.setWidth(5);
    Rect.setHeight(7);
    // Print the area of the object.
    Console.WriteLine("Total area: {0}", Rect.getArea());
    Console.ReadKey();
}
}
}
```

On executing the code shown above, the following result can be achieved.

Total area: 35

### Initialization of a Base Class

As you know, the derived class will inherit the member methods and member variables of the base class. As such, it is necessary to create the super class object before the creation of the subclass. Instructions for the initialization of the superclass can be provided in the member initialization list.

The following example illustrates this.

```
using System;

namespace RectangleApplication
{
    class Rectangle
    {
        //member variables
        protected double length;
        protected double width;
        public Rectangle(double l, double w)
        {
            length = l;
            width = w;
        }
        public double GetArea()
        {
            return length * width;
        }
        public void Display()

```

```
{
    Console.WriteLine("Length: {0}", length);
    Console.WriteLine("Width: {0}", width);
    Console.WriteLine("Area: {0}", GetArea());
}
}
//end class Rectangle

class Tabletop : Rectangle
{
    private double cost;
    public Tabletop(double l, double w) : base(l, w)
    {}
    public double GetCost()
    {
        double cost;
        cost = GetArea() * 70;
        return cost;
    }
}
```

```
public void Display()
{
    base.Display();
    Console.WriteLine("Cost: {0}", GetCost());
}
}

class ExecuteRectangle
{
    static void Main(string[] args)
    {
        Tabletop t = new Tabletop(4.5, 7.5);
        t.Display();
        Console.ReadLine();
    }
}
}
```

After the above code has been executed, the following result is achieved.

Length: 4.5

Width: 7.5

Area: 33.75

Cost: 2362.5

### C# and Multiple Inheritance

Multiple inheritances are not supported by C#. On the other hand, it is possible to use interfaces in order to implement multiple inheritances. This is demonstrated by the following example.

```
using System;

namespace InheritanceApplication
{
    class Shape
    {
        public void setWidth(int w)
        {
            width = w;
        }
        public void setHeight(int h)
```




{
    height = h;
}

protected int width;

protected int height;
}

// Base class PaintCost
public interface PaintCost
{
    int getCost(int area);
}

// Derived class
class Rectangle : Shape, PaintCost
{
    public int getArea()
    {
        return (width * height);
    }
}
}
public int getCost(int area)
{
    return area * 70;
}
}
class RectangleTester
{
    static void Main(string[] args)
    {
        Rectangle Rect = new Rectangle();
        int area;
        Rect.setWidth(5);
        Rect.setHeight(7);
        area = Rect.getArea();
        // Print the area of the object.
        Console.WriteLine("Total area: {0}", Rect.getArea());
    }
}

## 第12章

### 使用构造函数和析构函数

在本书中，你已经遇到过这两个术语。它们并不难掌握。在这里，我们将逐一探讨它们。

### C# 中的构造函数

类的构造函数可以说是该类的一个特殊成员函数。每当该类创建新对象时，它就会执行。构造函数与其类具有完全相同的名称，并且没有返回类型。

下面的示例演示了构造函数。

```
using System;

namespace LineApplication
{

class Line
{
```

```
private double length;  // Length of a line

public Line()
{
    Console.WriteLine("Object is being created");
}

public void setLength( double len )
{
    length = len;
}

public double getLength()
{
    return length;
}

static void Main(string[] args)
{
    Line line = new Line();

    // set line length
```

```
line.setLength(6.0);

Console.WriteLine("Length  of  line  :  {0}", line.getLength());

Console.ReadKey();
}
}
}
```

执行上述代码后，会产生以下结果。

Object is being created

Length of line : 6

### 参数化构造函数

默认情况下，构造函数没有任何参数。尽管如此，你可以向构造函数添加参数。这些构造函数被称为参数化构造函数。借助这种技术，你可以在创建特定对象时为其赋初始值。下面的示例将向你展示如何操作。

```
using System;
```

```
namespace LineApplication
```

```
{
    class Line
    {
        private double length; // Length of a line
        public Line(double len) //Parameterized constructor
        {
            Console.WriteLine("Object is being created, length = {0}", len);
            length = len;
        }
        public void setLength( double len )
        {
            length = len;
        }
        public double getLength()
        {
            return length;
        }
    }
```

```
static void Main(string[] args)
{
    Line line = new Line(10.0);
    Console.WriteLine("Length    of    line    :    {0}", line.getLength());
    // set line length
    line.setLength(6.0);
    Console.WriteLine("Length    of    line    :    {0}", line.getLength());
    Console.ReadKey();
}
}
}
```

执行上述代码后，产生的结果如下。

Object is being created; length = 10

Length of line : 10

Length of line : 6

### C# 中的析构函数

与构造函数一样，析构函数也是类的一个特殊成员函数。然而，它只在该类的某个对象超出其指定作用域时执行。析构函数的名称与其类完全相同，但带有一个前缀波浪号（~）。析构函数不能返回值，也不能接受任何参数。析构函数可能非常有用，因为它们可以在程序退出前释放内存资源。析构函数不能被继承。

下面的示例演示了析构函数的用法。

```
using System;

namespace LineApplication
{
    class Line
    {
        private double length; // Length of a line
        public Line() // constructor
        {
            Console.WriteLine("Object is being created");
        }
    }
```

```
~Line() // destructor
{
    Console.WriteLine("Object is being deleted");
}

public void setLength( double len )
{
    length = len;
}

public double getLength()
{
    return length;
}

static void Main(string[] args)
{
    Line line = new Line();
    // set line length
    line.setLength(6.0);
```

```
Console.WriteLine("Length  of  line  :  {0}",
line.getLength());

}

}
}
```

执行上述示例中的代码后，产生的结果如下。

Object is being created

Length of line : 6

Object is being deleted

现在你已经了解了什么是构造函数和析构函数。当你开始编写复杂程序时，你一定会发现它们很有用。因此，请确保你透彻理解它们。

## 第13章

### 深入了解接口与多态

这是两个你应该尽早熟悉的概念。它们将对你今后开发 C# 程序大有帮助。

### 接口简介

接口可以定义为一种语法契约，所有继承该接口的类都必须遵循它。接口定义契约的“什么”部分。派生类将定义语法契约的“如何”部分。

接口将定义作为其成员的方法、属性和事件。另一点需要注意的是，接口只包含成员的声明。定义成员的责任交给派生类。因此，它确保了存在一个可供派生类遵循的标准结构。

### 声明接口

可以使用 interface 关键字声明接口。实际上，它与类的声明有相似之处。默认情况下，接口语句是公共的。下面的示例演示了如何声明接口。

```
public interface ITransactions
{
	// interface members
	void showTransaction();
	double getAmount();
}
```

现在让我们通过一个示例来理解如何实现上述接口。

```
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System;

namespace InterfaceApplication
{
```

```
public interface ITransactions
{
    // interface members
    void showTransaction();
    double getAmount();
}

public class Transaction : ITransactions
{
    private string tCode;
    private string date;
    private double amount;
    public Transaction()
    {
        tCode = "";
        date = "";
        amount = 0.0;
    }
    public Transaction(string c, string d, double a)
```

```
{
    tCode = c;
    date = d;
    amount = a;
}
public double getAmount()
{
    return amount;
}
public void showTransaction()
{
    Console.WriteLine("Transaction: {0}", tCode);
    Console.WriteLine("Date: {0}", date);
    Console.WriteLine("Amount: {0}", getAmount());
}
}
class Tester
{
```

```
static void Main(string[] args)
{
    Transaction t1 = new Transaction("001", "8/10/2012", 78900.00);
    Transaction t2 = new Transaction("002", "9/10/2012", 451900.00);
    t1.showTransaction();
    t2.showTransaction();
    Console.ReadKey();
}
}
}
```

执行上述代码后，会产生以下结果。

Transaction: 001

Date: 8/10/2012

Amount: 78900

Transaction: 002

Date: 9/10/2012

### 开始了解多态

从字面上看，多态可以定义为具有多种形态。然而，在面向对象编程方法中，多态通常被描述为拥有一个接口但具有多个函数。现在，多态可以是静态的，也可以是动态的。

### 静态多态

静态绑定是程序编译时将函数与对象关联起来的机制。换句话说，该决定是在编译时做出的。在 C# 中，可以通过两种技术实现静态多态。

- 函数重载
- 运算符重载

下面的示例演示了函数重载。

下面的示例展示了使用 print() 函数打印不同的数据类型：

```
using System;
```

```
namespace PolymorphismApplication
```

```
{
```



class Printdata
{
    void print(int i)
    {
        Console.WriteLine("Printing int: {0}", i);
    }

    void print(double f)
    {
        Console.WriteLine("Printing float: {0}", f);
    }

    void print(string s)
    {
        Console.WriteLine("Printing string: {0}", s);
    }

    static void Main(string[] args)
    {
        Printdata p = new Printdata();
        // Call print to print integer
p.print(5);

// Call print to print float

p.print(500.263);

// Call print to print string

p.print("Hello C++");

Console.ReadKey();

}

}

}
执行上面所示的代码后，得到以下结果。

Printing int: 5

Printing float: 500.263

Printing string: Hello C++

### Dynamic Polymorphism

这种多态性中，决策将在运行时做出。这是通过方法重写实现的。

通过方法重写，可以在派生类和基类中拥有具有相同参数和相同名称的方法。因此，可以在运行时通过基类的对象指向派生类。

以下示例说明了动态多态性的使用。

```
using System;
namespace PolymorphismApplication
{
	class Shape
	{
		protected int width, height;
		public Shape(int a=0, int b=0)
		{
			width = a;
			height = b;
		}
		public virtual int area()
		{
			Console.WriteLine("Parent class area :");
			return 0;
		}
	}
}
```
}
}

class Rectangle: Shape
{
    public Rectangle( int a=0, int b=0): base(a, b)
    {
    }

    public override int area ()
    {
        Console.WriteLine("Rectangle class area :");
        return (width * height);
    }
}

class Triangle: Shape
{
    public Triangle(int a = 0, int b = 0): base(a, b)
    {
    }

public override int area()
{
    Console.WriteLine("Triangle class area :");
    return (width * height / 2);
}
}
class Caller
{
    public void CallArea(Shape sh)
    {
        int a;
        a = sh.area();
        Console.WriteLine("Area: {0}", a);
    }
}
class Tester
{
    static void Main(string[] args)
{
    Caller c = new Caller();
    Rectangle r = new Rectangle(10, 7);
    Triangle t = new Triangle(10, 5);
    c.CallArea(r);
    c.CallArea(t);
    Console.ReadKey();
    }
    }
}
编译并执行上面所示代码后产生的结果如下所示。

Rectangle class area:

Area: 70

Triangle class area:

Area: 25

至此，关于接口和多态性的章节就结束了。暂时不用担心使用它们。首先加强你在 C# 方面的基础。

## Chapter 14

### Learning the Basics of Debugging

即使你对计算机编程只有一点点了解，你也应该听说过调试。这是对所有种类软件和应用程序编程来说都至关重要的过程。你看，程序中可能存在错误。这些错误可能像打字错误或错误的语句那么简单。它们都被称作 bug，并且会阻止你的程序正确执行。因此这些 bug 需要被移除，而这正是通过调试实现的。

当你编写几行简单的应用程序时，例如本书中展示的示例，你很容易就能识别出错误。你只需简单地执行程序并找出 bug。然而，随着时间的推移，你肯定会开始编写更复杂的代码，代码长达数百行并且充满了复杂的语句。由于涉及的复杂程度很高，很难确定 bug 的位置。

在这些情况下，调试变得极其有用。因此，你必须花时间理解这个工具，才能成为更好的程序员。没有它，几乎不可能纠正复杂代码中发现的 bug。

### Understanding Print Debugging

最常用的调试类型被称为打印调试。虽然它是<|message|>最基本的调试类型，但由于其在某些情况下的有效性，往往会被高级程序员使用。

在打印调试中，让应用程序打印数字或文本。这使你能够找出代码的哪些部分已被执行以及变量中包含的内容。在 C# 中，Console.Write () 方法可用于打印状态消息或在控制台上显示特定变量的内容。

对于一些情况，这就足够了。另一方面，当你使用 Visual Studio 或甚至 Express 版本这样良好的 IDE 时，你将拥有更好的工具可以使用。好消息是，一旦了解基本原理，它们使用起来相当容易。

### Introduction to the Breakpoint

断点是你需要学习调试的第一件事。正如名称所示，断点标记代码中的特定点，在该点处其执行将暂停。

应用程序不会变得无用。相反，断点只是暂停应用程序的执行。

如果你使用 Visual Studio 或甚至 Express 版本，实现断点非常容易。在这些 IDE 中，你会注意到代码左侧有一个灰色区域。这被称为 gutter，在该区域左键单击会使一个红圈出现。这就是断点，调试器将在此点停止应用程序的执行。

这些只是调试的基础。随着你作为 C# 程序员的进步，你将自动了解到除最复杂的调试方面之外的各种其他调试工具和方法。

C#。因此，你不应该固守于特定的流程或技术。确实可能存在其他流程效果更好。

### Strengthen Your Base

你可能会学会编写代码，但你也必须知道每个概念或函数是如何结合在一起使代码工作的。换句话说，你需要彻底理解基础和基本原理。这将使你能够理解一段代码为何以这种方式工作，以及导致执行问题的可能 bug。因此，你将成为更好的开发者。

### Learn Some Advanced Ideas Extensively

当然，你不应该期望在开始学习 C# 几个月内就掌握所有高级技术和思想。然而，如果你花时间详细学习几个概念，这将极大地帮助你的进步。你应该在那几个概念上变得非常熟练。你可以自由选择想要专注的概念。它们可以是你工作中经常遇到的东西，也可以是你非常感兴趣的东西。试图在少数技术上成为专家，比试图掌握所有技术更容易。

### Take a Look at Code Written By Senior Programmers

学习 C# 中的概念和技术最好的方法之一是查看更有经验的程序员编写的代码。如果你在某个地方工作，你可以很容易地请资深程序员向你展示他们的代码。不要忘记理解他们为何使用某种技术以及他们如何使用它。或者，你可以浏览网上开源项目。它们不一定是顶尖程序员，但你仍然可以学到很多。当然，你必须避免盲目模仿他人所做的事情。只需理解思想并尝试在自己的代码中使用它。

## Conclusion

这标志着本书的结束。你现在拥有了面向对象编程语言 C# 的基础知识。你也学会了如何用这种语言编写一些基本程序，以及开始编写所需的内容。

你现在可以开始在代码中使用一些基本语句和方法。当然，你已经学会了如何声明和定义变量。更重要的是，你知道如何创建类，甚至在其中实现继承以创建代码块的层次结构。如果你愿意，你也可以开始在代码中实现条件逻辑，使其更高级，尤其是在循环和多个类的帮助下。

从本书中获得的信息足以帮助你开始 C# 编程。当然，还有更多需要了解和学习的内容。作为一种流行的编程语言，它会定期不断更新。因此，总会有新颖有趣的东西可学。在精通这种编程语言之后，



你也可以轻松开始学习其他令人惊叹的语言，如 C 甚至 Java 和 Ruby。你甚至可以踏入网页开发，因为 C# 是 .NET 框架的一部分。

我由衷感谢你选择这本书，希望它对你有所帮助。我也希望你能够建立一个坚实的基础，从中你可以将 C# 作为你的职业或爱好来发展。祝你在 C# 的学习和未来发展中一切顺利！

## 想了解更多编程知识？

查看 Joseph Connor 的其他书籍：

- **最新发行（2016 年 10 月）：** Programming: Computer Programming For Beginners: Learn The Basics Of HTML5, JavaScript, & CSS 或点击链接 https://www.amazon.com/dp/B01LYZGZKN
- **Python：** The Definitive Guide to Learning Python Programming for Beginners 或点击链接 https://www.amazon.com/dp/B013NLBAGC
- **Raspberry Pi 2：** The Definitive Beginner's Guide to Get Started with Raspberry Projects 或点击链接 https://www.amazon.com/dp/B013NKMD2Q
- **Hacking：** Hacking for Beginners - Computer Virus, Cracking, Malware, IT Security 或点击链接 https://www.amazon.com/dp/B010K7BVOQ
- **亚马逊畅销书：** Programming: Computer Programming for Beginners: Learn the Basics of Java, SQL & C++ - 3rd Edition 或点击链接 https://www.amazon.com/Programming-Computer-Beginners-Basics-JavaScript-ebook/dp/B014361TOM

查看我们的 Facebook 和 Instagram 以获取最新发行更新！

## 一本在约 100 页内教授 C# 的书？

快速高效地学习编程语言对初学者和专业人士都至关重要。

无论你是经验丰富的 C++ 程序员，还是正在努力成为一名全职程序员，C# 编程都是一项必备技能。C# 是一种通用编程语言，具有大量现实应用。它用于 Windows Silverlight、移动开发、游戏开发和第三方 Windows 应用。它设计精良，易于学习，使用愉快。

通过 *Computer Programming for Beginners: Learn the Basics of C#*，你将获得成为 C# 程序员所需的一切，包括：

- 如何设置你的电脑并启动一个新的 C# 项目
- 对数据类型和变量的基本理解
- 对关键编程原则的介绍
- 软件或应用开发的基本技术
- 面向对象编程中使用的基本概念
- 如何使用方法、数组、字符串、结构和枚举
- 对继承、接口和多态性的一般理解

逐章地，Joseph Connor 带你掌握掌握 C# 基础知识所需的所有关键概念。但本指南并不止于此。你还将学习调试的基础知识，并获得来自了解所有功能和细微差别的业内人士的丰富专家建议。

不要因为你还没有学习 C# 而错失完美的机会。今天就开始学习 *Computer Programming for Beginners: Learn the Basics of C#*。

立即向上滚动购买你的副本。
