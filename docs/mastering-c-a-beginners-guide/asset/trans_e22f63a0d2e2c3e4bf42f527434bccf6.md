

```
Console.WriteLine("Hello\nWorld!");
    }
  }
}
```

第1行，一条 using 指令向编译器表明，该源文件引用的是在 System 命名空间中声明的类和构造。第6行中的 public 关键字显示了该程序对其他应用程序或组件的可访问性范围。

在第7行，我们看到左花括号（“{”），它表示 SimpleHelloWorld 类主体的开始。属于类的所有内容，如字段、属性和方法，都出现在左右花括号之间的类主体中。Main() 方法中的 static 关键字表明，此方法无需实例化该类即可调用。

## 编译程序

可以将 C# 程序编译为程序集或模块。如果程序包含一个带有 Main() 方法的类，则可以直接编译为程序集。该文件带有“.exe”扩展名。没有 main() 方法的程序可以编译为模块，如下所示：

```
csc/target:module "program_name"
```

然后，你可以通过按 F9 或直接对源文件运行 C# 命令行编译器（csc.exe）来编译此程序，如下所示：

```
csc oops.cs
```

## *类和对象*

类可以视为特殊类型的模板，你可以从中创建对象。每个对象都有自己的数据以及操作和访问这些数据的方法。类定义了该类的每个对象可以包含的数据和功能。

类声明由类头和类主体组成。类头包含修饰符、属性和 class 关键字。类主体封装了类的成员，即数据成员和成员函数。类声明的语法如下：

- Attributes accessibility modifiers class identifier: baselist {body}

属性可以给类带来额外的上下文，就像形容词一样。下表列出了可访问性关键字：

| 关键字 | 描述 |
|---|---|
| Public | 公共类在当前程序集和引用程序集中可见。 |
| Private | 仅在当前类内可见。 |
| Protected | 在当前类和派生类内可见。 |
| Internal | 在包含程序集内可见。 |
| Internal protected | 在包含程序集内以及当前类的派生类中可见。 |

此外，你可以使用修饰符来细化类的声明。下表定义的所有修饰符列表如下：

| 修饰符 | 描述 |
|---|---|
| Sealed | 类不能被派生类继承。 |
| Static | 类仅包含静态成员。 |
| Unsafe | 该类具有某些不安全构造，如指针。 |
| Abstract | 如果类是抽象的，则不创建该类的实例。 |

## 多个类声明

有时需要在单个命名空间中声明多个类。因此，无需向解决方案中添加单独的类。相反，你可以将新类引入现有的 program.cs 或其他文件中，如下所示。

```
using System;
namespace oops
{
    class Program
    {
        public void MainFunction()
        {
            Console.WriteLine("Main class");
        }
        static void Main(string[] args)
```

```csharp
{
    //main class instance
    Program obj = new Program();
    obj.MainFunction();

    //other class instance
    demo dObj=new demo();
    dObj.addition();
}
}

class demo
{
    int x = 10;
    int y = 20;
    int z;

    public void addition()
    {
        z = x + y;
        Console.WriteLine("other class in Namespace");
        Console.WriteLine(z);
    }
}
}
```

在这里，在此示例中，我们在第12行的 program.cs 文件中创建了一个额外的类“demo”。然后，在第6到11行的 Main() 入口中，我们实例化了 demo 类以及 program 类。

## 分部类

通常，一个类会占用一个文件。但是，当多个开发人员需要访问同一个类时，将该类放在多个文件中会很有帮助。partial 关键字允许一个类跨多个源文件。编译时，分部类型的元素将被收集到一个程序集中。

定义分部类有一些规则，如下所示：

- 分部类型必须具有相同的可访问性。
- “partial”关键字位于每个分部类型之前。
- 如果分部类型是 sealed 或省略，则整个类将是 abstract。

在下面的示例中，我们包含两个文件：partial-Part1.cs 和 partialPart2.cs，并在两个类中都声明了一个分部类 partialclassDemo。

```
partialPart1.cs
using System;
namespace oops
{
    public partial class partialclassDemo
    {
        public void method1()
        {
            Console.WriteLine("method from
part1 class");
        }
    }
}
```

> [6] https://www.c-sharpcorner.com/UploadFile/84c85b/object-oriented-programming-using-C-Sharp-net/, C-sharpcorner

```csharp
partialPart2.cs
using System;
namespace oops
{
    public partial class partialclassDemo
    {
        public void method2()
        {
            Console.WriteLine("method from
part2 class");
        }
    }
}
```

最后，我们在 program.cs 文件中创建 partialclassDemo 的实例，如下所示：

```csharp
Program.cs
using System;
namespace oops
{
    class Program
    {
        static void Main(string[] args)
        {
            //partial class instance
            partialclassDemo obj = new
partialclassDemo();
            obj.method1();
            obj.method2();
        }
    }
}
```

## 静态类

静态类是使用“static”关键字声明的。如果类声明为静态，则编译器永远不会创建该类的实例。所有成员字段、属性和函数都应声明为静态，并通过类名直接访问，而不是通过类实例对象访问。用一个示例来说明：

```
using System;
namespace oops
{
    static class staticDemo
    {
        //static fields
        static int x = 10, Y;
        //static method
        static void calcute()
        {
            y = x * x;
            Console.WriteLine(y);
        }
        static void Main(string[] args)
        {
            //function calling directly
            staticDemo.calcute();
        }
    }
}
```

## 构造函数和析构函数

构造函数是一种用于初始化字段的特殊函数。构造函数与类同名。实例构造函数使用 new 运算符调用，并且不能像其他成员函数那样调用。关于构造函数，你需要了解一些重要规则：

- 没有构造函数的类具有一个隐式构造函数，称为默认构造函数，它是无参数的。
- 公共构造函数允许在当前程序集或引用程序集中创建对象。
- 只允许在构造函数上使用 extern 修饰符。
- 构造函数返回 void，但没有显式声明的返回类型。
- 构造函数可以有零个或多个参数。
- 类可以有多个构造函数，可以是默认、参数化或两者的形式。

下面的示例展示了一个 customer 类的构造函数：

```
using System;
namespace oops
{
    class customer
    {
        // Member Variables
        public string Name;
```

```
//constructor for initializing
fields
    public customer(string fname,
string lname)
    {
        Name= fname +" "+ lname;
    }
    //method for displaying customer
records
    public void AppendData()
    {
        Console.WriteLine(Name);
    }
    //Entry point
    static void Main(string[] args)
    {
        // object instantiation
        customer obj = new
customer("Barack", "Obama");

        //Method calling
        obj.AppendData();
    }
}
}
```

一旦执行 new 语句，就会调用默认构造函数。

## 静态构造函数

创建静态构造函数是为了初始化静态字段。静态构造函数不会随着 new 语句同时调用。它们在类首次被访问时调用。

