

## 构造函数链：使用 this 调用另一个构造函数

请注意，在清单 5.30 中，Employee 对象的初始化代码现在在多个地方重复，因此需要在多个地方进行维护。代码量虽小，但可以通过从一个构造函数调用另一个构造函数——即构造函数链——使用构造函数初始化器来消除重复。构造函数初始化器在执行当前构造函数的实现之前确定要调用哪个构造函数（参见清单 5.31）。

### 清单 5.31：从一个构造函数调用另一个构造函数

```
class Employee
{
    public Employee(string firstName, string lastName)
    {
        FirstName = firstName;
        LastName = lastName;
    }

    public Employee(
        int id, string firstName, string lastName )
        : this(firstName, lastName)
    {
        Id = id;
    }

    public Employee(int id)
    {
        Id = id;

        // Look up employee name...
        // ...
    }

    // NOTE: Member constructors cannot be
    // called explicitly inline
    // this(id, firstName, lastName);

    public int Id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Salary { get; set; }

    // ...
}
```

要在同一个类中（针对同一对象实例）从一个构造函数调用另一个构造函数，C# 使用冒号，后跟 this 关键字，再后跟被调用构造函数声明中的参数列表。在这种情况下，接受三个参数的构造函数会调用接受两个参数的构造函数。通常，调用模式是相反的；参数最少的构造函数会调用参数最多的构造函数，并为未知参数传递默认值。

### 初学者主题

### 集中初始化

请注意，在清单 5.31 中 Employee(int id) 构造函数的实现里，你不能调用 this(firstName, lastName)，因为该构造函数不存在此类参数。要实现所有初始化代码都通过一个方法来处理的模式，你必须创建一个单独的初始化方法，如清单 5.32 所示。

### 清单 5.32：提供初始化方法

```
class Employee
{
    public Employee(string firstName, string lastName)
    {
        int id;
        // Generate an employee ID...
        // ...
        Initialize(id, firstName, lastName);
    }

    public Employee(int id, string firstName, string lastName )
    {
        Initialize(id, firstName, lastName);
    }

    public Employee(int id)
    {
        string firstName;
        string lastName;
        Id = id;

        // Look up employee data
        // ...

        Initialize(id, firstName, lastName);
    }

    private void Initialize(
        int id, string firstName, string lastName)
    {
        Id = id;
        FirstName = firstName;
        LastName = lastName;
    }

    // ...
}
```

在这种情况下，该方法名为 Initialize()，它同时接受姓名和员工 IDs。请注意，你可以继续从一个构造函数调用另一个构造函数，如清单 5.31 所示。

### 高级主题

### 匿名类型

C# 3.0 引入了对匿名类型的支持。这些数据类型由编译器（即时）生成，而不是通过显式类定义。清单 5.33 显示了这样的声明。

### 清单 5.33：带匿名类型的隐式局部变量

```
using System;

class Program
{
    static void Main()
    {
        var patent1 =
            new
            {
                Title = "Bifocals",
                YearOfPublication = "1784"
            };

        var patent2 =
            new
            {
                Title = "Phonograph",
                YearOfPublication = "1877"
            };

        var patent3 =
            new
            {
                patent1.Title,
                Year = patent1.YearOfPublication
            };

        System.Console.WriteLine("() ({1})",
            patent1.Title, patent1.YearOfPublication);
        System.Console.WriteLine("() ({1})",
            patent2.Title, patent2.YearOfPublication);

        Console.WriteLine();
        Console.WriteLine(patent1);
        Console.WriteLine(patent2);

        Console.WriteLine();
        Console.WriteLine(patent3);
    }
}
```

### 输出 5.8：

```
Bifocals (1784)
Phonograph (1877)
{ Title = Bifocals, YearOfPublication = 1784 }
{ Title = Phonograph, YearOfPublication = 1877 }
{ Title = Bifocals, Year = 1784 }
```

清单 5.33 演示了将匿名类型赋值给隐式类型（var）局部变量。

当编译器遇到匿名类型语法时，它会生成一个 CIL 类，其中包含与匿名类型声明中的命名值和数据类型相对应的属性。虽然 C# 中没有可用于生成类型的名称，但它仍然是静态类型的。例如，该类型的属性完全可访问。在清单 5.33 中，patent1.Title 和 patent2.YearOfPublication 在 Console.WriteLine() 语句中被调用。任何尝试调用不存在的成员都会导致编译错误。即使是 Visual Studio 2008 等 IDE 中的 IntelliSense 也支持匿名类型。

在清单 5.33 中，匿名类型上的成员名称是通过将值赋给名称来显式标识的（参见 patent1 和 patent2 赋值中的 Title 和 YearOfPublication）。但是，如果赋值的是属性或字段，且未显式指定名称，则名称将默认为字段或属性的名称。例如，patent3 是使用属性名称“Title”而不是赋值给隐式名称来定义的。如输出 5.8 所示，生成的属性名称由编译器确定，以匹配检索值的属性。

虽然编译器允许像清单 5.33 中所示的匿名类型声明，但通常应避免使用匿名类型声明，甚至避免使用与 var 相关的隐式类型，除非你正在处理关联不同类型数据的 lambda 和查询表达式，或者你正在水平投影数据，使得对于特定类型，整体数据更少。直到从集合中频繁查询数据使得显式类型声明变得繁琐之前，最好像本章所述那样显式声明类型。

## 静态成员

第 1 章中的 HelloWorld 示例首次介绍了 static 关键字；但是，它并未完全定义它。本节将完全定义 static 关键字。

首先，考虑一个示例。假设员工 Id 值需要对每个员工都是唯一的。实现此目的的一种方法是存储一个计数器来跟踪每个员工 ID。但是，如果该值作为实例字段存储，那么每次实例化对象时，都会创建一个新的 NextId 字段，导致 Employee 对象的每个实例都会为该字段消耗内存。最大的问题是，每次实例化 Employee 对象时，之前实例化的所有 Employee 对象上的 NextId 值都需要用下一个 ID 值进行更新。你需要的是一个由所有 Employee 对象实例共享的单个字段。

### 语言对比：C++/Visual Basic—全局变量和函数

与之前的许多语言不同，C# 没有全局变量或全局函数。C# 中的所有字段和方法都出现在类的上下文中。在 C# 领域中，全局字段或函数的等价物是静态字段或函数。全局变量/函数与 C# 静态字段/方法之间没有功能差异，除了静态字段/方法可以包含访问修饰符（例如 private），这些修饰符可以限制访问并提供更好的封装性。

### 静态字段

要定义可在多个实例中使用的数据，请使用 static 关键字，如清单 5.34 所示。

### 清单 5.34：声明静态字段

```
class Employee
{
    public Employee(string firstName, string lastName)
    {
        FirstName = firstName;
        LastName = lastName;
        Id = NextId;
        NextId++;
    }

    // ...

    public static int NextId;
    public int Id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Salary { get; set; }

    // ...
}
```

在此示例中，NextId 字段声明包含 static 修饰符，因此称为静态字段。与 Id 不同，NextId 的单个存储位置在所有 Employee 实例之间共享。在 Employee 构造函数内部，你将新 Employee 对象的 Id 赋值为 NextId 的值

