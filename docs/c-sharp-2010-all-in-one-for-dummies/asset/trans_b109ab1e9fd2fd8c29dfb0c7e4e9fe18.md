
下面是初始化器相关的内容。`_accountNumber` 和 `_balance` 都在声明时被赋值，这与构造函数具有相同的效果，但不必在构造函数中完成这项工作。

要弄清楚到底发生了什么。你可能会认为这条语句现在就把 `_balance` 设为 0.0。然而，`_balance` 只作为对象的一部分存在。因此，只有在创建 BankAccount 对象之后，该赋值才会执行。事实上，每次创建对象时都会执行该赋值。

注意，静态数据成员 `_nextAccountNumber` 在首次访问 BankAccount 类时初始化——正如你在调试器中的演练所示，那是你首次访问拥有该静态数据成员的对象的任何方法或属性，包括构造函数。

静态成员初始化之后，每次构造 BankAccount 实例时都不会重新初始化。这一点与非静态成员不同。

初始化器按其在类声明中出现的顺序执行。如果 C# 同时遇到初始化器和构造函数，则初始化器在构造函数体之前执行。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_307_0.png)

### 观察带初始化器的构造过程

在 DemonstrateCustomConstructor 程序中，将 `new MyOtherObject()` 调用从 MyObject 构造函数移到声明本身，如下所示（见粗体文本），按所示修改第二个 `WriteLine()` 语句，然后重新运行程序：

```csharp
public class MyObject
{
    // This member is a property of the class (it's static).
    private static MyOtherObject _staticObj = new MyOtherObject();
    // This member is a property of each instance.
    private MyOtherObject _dynamicObj = new MyOtherObject(); // <-- Here.
    public MyObject()
    {
        Console.WriteLine("MyObject constructor starting");
        Console.WriteLine("Both data members initialized before this constructor");
        // _dynamicObj construction was here, now moved up.
        Console.WriteLine("MyObject constructor ending");
    }
}
```

将修改后程序的以下输出与其前身 DemonstrateCustomConstructor 的输出进行比较：

```text
Main() starting
Creating a local MyObject in Main():
MyOtherObject constructing
MyOtherObject constructing
MyObject constructor starting
(Both data members initialized before this constructor)
MyObject constructor ending
Press Enter to terminate...
```

你可以在网站上找到整个程序（完成这些更改后），其大名是 DemonstrateConstructorWithInitializer。

### 新特性：无需构造函数初始化对象

假设你有一个表示 Student 的小类：

```csharp
public class Student
{
    public string Name { get; set; }
    public string Address { get; set; }
    public double GradePointAverage { get; set; }
}
```

Student 对象有三个公共属性：Name、Address 和 GradePointAverage，它们指定学生的基本信息。

通常，创建新的 Student 对象时，必须像这样初始化其 Name、Address 和 GradePointAverage 属性：

```csharp
Student randal = new Student();
randal.Name = "Randal Sphar";
randal.Address = "123 Elm Street, Truth or Consequences, NM 00000";
randal.GradePointAverage = 3.51;
```

（是的，弗吉尼亚，新墨西哥州确实有个地方叫 Truth or Consequences。我的侄子 Randal 出生在那里。）

如果 Student 有构造函数，你可以这样做：

```csharp
Student randal = new Student
("Randal Sphar", "123 Elm Street, Truth or Consequences, NM 00000", 3.51);
```

然而遗憾的是，除了 C# 自动提供的默认构造函数（不接受参数）之外，Student 没有其他构造函数。

在 C# 3.0 及更高版本中，你可以用某种看起来可疑地像构造函数的东西来简化该初始化——嗯，算是吧：

```csharp
Student randal = new Student
{
    Name = "Randal Sphar",
    Address = "123 Elm Street, Truth or Consequences, NM 00000",
    GradePointAverage = 3.51
};
```

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_308_0.png)

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_308_1.png)

最后两个示例在这一点上不同：第一个使用构造函数，显示的是括号中包含两个字符串和一个 double 值，以逗号分隔；第二个使用新的对象初始化器语法，改用花括号包含三个赋值，以逗号分隔。该语法大致如下：

```csharp
new LatitudeLongitude
{ assignment to Latitude, assignment to Longitude };
```

新的对象初始化器语法允许你在代码块（花括号）中为 LatitudeLongitude 对象的任何可访问的 set 属性赋值。该代码块用于初始化对象。注意，通过这种方式只能设置可访问的属性，不能设置私有属性，也不能在初始化器中调用对象的任何方法或执行任何其他工作。

新语法简洁得多：一条语句对三条语句。而且，它简化了创建已初始化对象的过程，而这些对象无法通过构造函数做到这一点。（我把 Student 示例分成多行只是为了适合页面——那只是因为 Truth or Consequences 这个名字很长。如果你住在那儿，它看起来会更长。）

新的对象初始化器语法除了方便之外，并不会给你带来太多其他好处，但在编码时，方便性在任何程序员的清单上都名列前茅。简洁也是如此。此外，当你阅读匿名类相关内容时，这个特性会变得必不可少。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_309_0.png)

尽情使用新的对象初始化器语法吧。在本书其余部分，我自己也经常使用它。

在帮助中查找术语 object initializer，以找到关于它适用于哪些种类属性的律师式措辞。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_309_1.png)

网站上的 ObjectInitializers 程序示例演示了对象初始化器。

## 第6章：继承：我能得到的就这些吗？

### 本章内容

- 依据另一个更基础的类来定义一个类
- 区分 *is a* 与 *has a*
- 用一个类对象替代另一个类对象
- 构造静态成员或实例成员
- 在继承层次结构中包含构造函数
- 专门调用基类构造函数

面向对象编程基于四项原则：控制访问的能力（封装）、从其他类继承、恰当地响应（多态），以及间接地从一个对象引用另一个对象（接口）。

继承是一个常见的概念。我是人类，除了刚醒来的时候。我从 `Human` 类继承某些属性，比如我或多或少能交谈的能力，以及我对空气、食物和含大量咖啡因的碳水化合物饮料的依赖。`Human` 类从 `Mammal` 类继承对空气、水和营养的依赖，而 `Mammal` 类又继承自 `Animal` 类。

传递属性的能力是一种强大的能力。你可以用它以经济的方式来描述事物。例如，如果我儿子问：“鸭子是什么？”我可以说：“是一种会嘎嘎叫的鸟。”不管你怎么想，这个答案传达了相当多的信息。我儿子知道鸟是什么，现在他知道了鸭子所有相同的特征，外加鸭子“嘎嘎叫”这一额外属性。

面向对象语言通过允许一个类从另一个类继承属性来表达这种继承关系。这一特性使面向对象语言能够生成比不支持继承的语言所生成的模型更接近现实世界的模型。

### 类继承

在下面的 InheritanceExample 程序中，SubClass 类继承自 BaseClass 类：

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_311_0.png)

```csharp
// InheritanceExample -- Provide the simplest possible
// demonstration of inheritance.
using System;
namespace InheritanceExample
{
    public class BaseClass
    {
        public int _dataMember;
        public void SomeMethod()
        {
            Console.WriteLine("SomeMethod()");
        }
    }
    public class SubClass : BaseClass
    {
        public void SomeOtherMethod()
        {
            Console.WriteLine("SomeOtherMethod()");
        }
    }
    public class Program
    {
        public static void Main(string[] args)
        {
            // Create a base class object.
            Console.WriteLine("Exercising a base class object:");
            BaseClass bc = new BaseClass();
            bc._dataMember = 1;
            bc.SomeMethod();
            // Now create a subclass object.
            Console.WriteLine("Exercising a subclass object:");
            SubClass sc = new SubClass();
            sc._dataMember = 2;
            sc.SomeMethod();
            sc.SomeOtherMethod();
            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
    }
}
```

BaseClass 类定义了一个数据成员和简单方法 `SomeMethod()`。`Main()` 创建并使用了 BaseClass 对象 bc。

SubClass 类通过在类定义中的冒号后放置类名 BaseClass 来继承该类：

```csharp
public class SubClass : BaseClass
```
