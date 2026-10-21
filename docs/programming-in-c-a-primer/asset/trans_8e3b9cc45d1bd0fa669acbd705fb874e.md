

# Program 3.1 | 一个简单的 C# 程序

```
class SampleOne
{
    public static void Main()
    {
        System.Console.WriteLine("C# is sharper than C++.");
    }
}
```

程序 3.1 是所有 C# 程序中最简单的一个。尽管如此，它展示了该语言的许多显著特性。因此，让我们逐行讨论这个程序，并理解构成一个 C# 程序的独特特性。

## 3.2.1 类声明

第一行

    class SampleOne

声明了一个类，这是一种面向对象的构造。如前所述，C# 是一种真正的面向对象语言，因此“一切”都必须放在类中。class 是一个关键字，表示后面将是一个新的类定义。SampleOne 是一个 C# 标识符，用于指定要定义的类的名称。

类是描述对象的外观和行为方式的模板。（关于类的更多内容将在第 12 章讨论。）

## 3.2.2 大括号

C# 是一种块结构语言，意味着代码块总是用大括号 `{` 和 `}` 括起来。因此，C# 中的每个类定义都以左大括号 `{` 开始，并以程序最后一行中对应的右大括号 `}` 结束。这与 Java 和 C++ 的类构造类似。注意，右大括号后面没有分号。

## 3.2.3 Main 方法

第三行

    public static void Main()

定义了一个名为 Main 的方法。每个 C# 可执行程序都必须在其某个类中包含 Main() 方法。这是程序执行的“起点”。一个 C# 应用程序可以有任意数量的类，但“只有一个”类可以包含 Main 方法来启动执行。注意，C# 组件库根本不会使用 Main 方法。

这一行包含几个关键字：public、static 和 void。这与 C++ 和 Java 中的 main 非常相似。与 Java 和 C++ 不同，Main 中的 M 是大写而不是小写。这些关键字的含义和用途如下：

| public | 关键字 public 是一个访问修饰符，它告诉 C# 编译器 Main 方法可以被任何人访问 |
| static | 关键字 static 声明 Main 方法是一个全局方法，无需创建类的实例即可调用。编译器将该方法的地址存储为入口点，并在创建任何对象之前利用此信息开始执行。 |

C# 支持一种称为 using 指令的特性，可用于将 System 命名空间导入到程序中。一旦导入了命名空间，我们就可以使用该命名空间中的元素，而无需使用命名空间作为前缀。程序 3.2 对这一点进行了说明。

# Program 3.2 | 使用命名空间和注释的程序

```
/*
This program uses namespaces and comment lines
*/
using System; // System is a namespace
class SampleTwo
{
    // Main method begins
    public static void Main()
    {
        Console.WriteLine("Hello!");
    }
    // Main method ends
}
```

注意，程序中的第一条语句是 using System;

这告诉编译器在 System 库中查找未解析的类名。注意，在输出行中，我们没有在 Console 类前使用 System 前缀。

当编译器解析 Console.WriteLine 方法时，它会发现该方法未定义。然后，它会在 using 指令指定的命名空间中搜索，一旦在 System 命名空间中找到该方法，就会在编译代码时不报告任何错误。

## 3.4 添加注释

注释在程序维护中起着非常重要的作用。它们用于提高代码的可读性和理解性。所有程序都应包含实现细节、变更历史以及所执行任务等信息。C# 允许两种类型的注释，即：

- 单行注释
- 多行注释

程序 3.2 演示了这两种方法的使用。

单行注释以双反斜杠（//）符号开头，到行尾结束。我们可以将 // 单独放在一行，也可以放在代码语句之后。它还可以用于注释掉源代码的整行或部分行。一行中 // 之后的所有内容都被视为注释。

// This is an example of
// Multiline comments
// in C# language

/* */ 是 C# 的一种注释类型，但使用时有一个注意事项。考虑下面的代码段：

由于开始符号和结束符号不匹配，这会导致错误。也就是说，我们不能嵌套 /* */ 注释。每个 /* 符号都应该有对应的 */ 符号。

## 3.5 Main 返回一个值

另一个重要方面是 Main() 的返回类型。在前面的程序中，我们使用了 void 作为返回类型。如果 Main() 声明为 int 类型而不是 void，它也可以返回一个值。当返回类型为 int 时，必须在方法末尾包含一条 return 语句，如程序 3.3 所示。

# Program 3.3 | 返回值的 Main

```
// Main returning a value
using System;
class SampleThree
{
    public static int Main()
    {
        Console.WriteLine("Hello!");
        return 0; // Return statement
    }
}
```

程序 3.3 向系统返回一个整数值。返回的值作为程序的终止状态代码。该代码的目的是允许向执行环境传达成功或失败的信息。

## 3.6 为命名空间类使用别名

我们已经看到如何通过使用 using System; 语句来避免在 Console 类前添加 System 前缀。能否用同样的方法避免在 WriteLine() 方法前添加 System.Console 前缀？答案是“不能”。

System 是一个命名空间，Console 是一个类。using 指令只能应用于命名空间，不能应用于类。因此，using System.Console; 语句是非法的。不过，我们可以通过为命名空间类使用别名来克服这个问题。其形式如下：

```
using alias-name = class-name;
```

程序 3.4 演示了类别名的使用。

# Program 3.4 类别名的使用

```
using A = System.Console; //A is alias for System.Console
class SampleFour
{
    public static void Main()
    {
        D.WriteLine("Hello!");
    }
}
```

## 3.7 向 WriteLine 方法传递字符串对象

到目前为止，我们只看到了向 Console 输出常量字符串。我们可以将字符串值存储在字符串对象中，并将这些对象作为 WriteLine 方法的参数。我们可以使用 string 数据类型创建字符串变量，并为其赋值一个字符串常量，如下所示：

```
string s = "abc";
```

s 的内容可以使用 WriteLine 方法打印出来。
System.Console.WriteLine(s); //s is string object
程序 3.5 演示了将字符串对象作为输出方法 WriteLine 的参数使用。

# Program 3.5 在输出中使用字符串对象

```
using System;
class SampleFive
{
    public static void Main()
    {
        string name = "C sharp"; // name is assigned a string
        Console.WriteLine(name);
    }
}
```

## 3.8 命令行参数

有些时候，我们希望程序根据执行时提供的输入以特定方式运行。在 C# 中，这是通过使用所谓的命令行参数来实现的。命令行参数是在调用 Main 方法执行时提供给它的参数。程序 3.6 从命令行接受一个名称并将其写入控制台。

# Program 3.6 命令行参数

```
/*
This program uses command line arguments as input
*/
using System;
class SampleSix
{
public static void Main (string [] args)
{
Console.Write("welcome to");
Console.Write(" " +args[0]);
Console.WriteLine(" " +args[1]);
}
}
```

在前面的示例中，我们使用了不带参数的 Main 方法。注意在这个示例中 Main 是如何声明的。

```
public static void Main (string [] args)
```

Main 声明时带有一个参数 args。参数 args 被声明为字符串数组（即字符串对象数组）。执行时在命令行中提供的任何参数都会作为元素传递给数组 args。我们可以使用下标（如 args[0]、args[1] 等）访问数组元素。例如，考虑如下命令行：

SampleSix C sharp

这个命令行包含两个参数，它们被赋值给数组 args，如下所示：

- C → args[0]
- sharp → args[1]

注意，C# 下标从 0 开始，而不是从 1 开始。（数组和字符串将在后面详细讨论。）如果使用上述命令行执行程序 3.6，将得到以下输出：

Welcome to C sharp

注意这里使用了一个新的输出方法 Console.Write()。

它与 WriteLine() 方法唯一的区别是 Write() 不会产生换行，因此下一条输出语句会打印在同一行。这样，三条输出语句合在一起产生一行输出。有关输出格式的更多细节，请参阅第 17 章。

注意输出语句在打印时如何使用 + 运算符连接字符串。这里使用空字符串在字符串之间提供空白。（+ 运算符被重载以执行两个字符串相加的任务。有关运算符重载的更多细节，请参阅第 15 章。）

程序 3.7 展示了在 C# 中使用命令行参数的另一个示例。该程序计算作为命令行参数传入的数字的平方根并显示输出。

# Program 3.7 | 命令行示例

```
using System;
class CommandLineExample
{
static void Main(string[] args)
{
double argValue=0.0;
double sqrtValue=0.0;
if (args.Length == 0)
{
Console.WriteLine("Please enter a number");
}
else
{
argValue = double.Parse(args[0]);
sqrtValue = Math.Sqrt(argValue);
Console.WriteLine("Square root of " + argValue + " is " + sqrtValue);
}
}
}
```

