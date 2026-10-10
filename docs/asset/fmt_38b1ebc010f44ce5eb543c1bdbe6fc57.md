
![](img/6df7bb88e9302e98442acc219cfbd7fc_292_0.png)

![](img/6df7bb88e9302e98442acc219cfbd7fc_292_1.png)

![](img/6df7bb88e9302e98442acc219cfbd7fc_292_2.png)

## 让编译器为你编写属性 (Letting the compiler write properties)

上一节描述的大多数属性都是完全常规的，编写它们很繁琐（尽管简单）：

```c
private string _name; // 属性的数据成员
public string Name { get { return _name; } set { _name = value; } }
```

由于反复编写相同的模板代码，从 C# 3.0 开始，现在由编译器为你完成。你为属性（包括私有数据成员）只需要编写这一行：

```csharp
public string Name { get; set; }
```

这一行等同于：

```c
private string <somename>; // <somename> 是什么？不知道也不在乎。
public string Name { get { return <somename>; } set { <somename> = value; } }
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_293_0.png)

编译器会创建一个无名的数据成员，连同访问器的模板代码。`csharp102.info` 上的 `AccessorPropertyShortcuts` 示例演示了这种用法。这种风格鼓励即使在所在类的其他成员内部使用属性，因为你只知道属性名称。因此，当你编写快捷属性时，必须同时拥有 `get` 和 `set`。你可以使用属性语法初始化此类属性：

```csharp
public int AnInt { get; set; } // 编译器提供了一个私有变量。
...
AnInt = 2; // 通过属性初始化编译器生成的实例变量。
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_293_1.png)

## 带访问级别的访问器 (Accessors with access levels)

访问器属性并不一定需要声明为 `public`。如果访问器仅在类内部使用，你可以将其声明为任何适当级别，即使是 `private`。（接下来的示例将 `Name` 属性标记为 `internal`。）

你甚至可以单独调整访问器中 `get` 和 `set` 部分的访问级别。假设你不想在类外部暴露 `set` 访问器——它仅供内部使用。你可以像这样写该属性：

```
internal string Name { get; private set; }
```

`csharp102.info` 上的 `AccessorPropertyShortcuts` 示例说明了这种用法。

# 让你的对象有一个良好的开始 —— 构造函数

控制类的访问只解决了一部分问题：如果一个对象想要成长，它的生命之初有一个良好的开始。类可以提供一个初始化方法，由应用程序调用以启动程序，但应用程序可能会忘记调用该方法。类将从垃圾数据开始，此后情况并不会好转。如果你想对该类负责，就必须确保它有机会正确地启动。

C# 通过自动为你调用初始化方法来解决这个问题——例如：

```
MyObject mo = new MyObject();
```

换句话说，这条语句不仅从特殊的内存区域获取一个对象，还初始化了该对象的成员。

在脑海中保持“类”和“对象”这两个术语分开。猫（`Cat`）是一个类。我的猫 `Striper` 是 `Cat` 类的一个对象。

## C# 提供的构造函数

C# 会跟踪变量是否已经初始化，并不允许你使用未初始化的变量。例如，下面的代码段会产生编译时错误：

```
public static void Main(string[] args)
{
    int n;
    double d;
    double calculatedValue = n + d;
}
```

C# 记录了局部变量 `n` 和 `d` 未被赋值的这一事实，并不允许在表达式中使用它们。编译这个微型程序会产生这些编译器错误：

```
Use of unassigned local variable 'n'
Use of unassigned local variable 'd'
```

相比之下，C# 提供了一个*默认构造函数*，它将将的*数据成员*初始化为：

- 数字类型为 0
- 布尔类型为 false
- 对象引用为 null

考虑以下简单的程序示例：

```csharp
using System;
namespace Test
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // 先创建一个对象。
            MyObject localObject = new MyObject();
            Console.WriteLine("localObject.n is {0}", localObject.n);
            if (localObject.nextObject == null)
            {
                Console.WriteLine("localObject.nextObject is null");
            }
            // 等待用户确认结果。
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
    }
    public class MyObject
    {
        internal int n;
        internal MyObject nextObject;
    }
}
```

该程序定义了一个类 `MyObject`，它包含一个 `int` 类型的简单数据成员 `n` 和一个指向对象的引用 `nextObject`（两者都声明为 `internal`）。`Main()` 方法创建了一个 `MyObject`，然后显示 `n` 和 `nextObject` 的初始内容。

执行该程序的输出如下：

```
localObject.n is 0
localObject.nextObject is null
Press Enter to terminate...
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_296_0.png)

在值创建时初始化它的代码就是默认构造函数。它“构建”了该类，从初始化成员成员意义上说是这样。因此，C# 确保对象从已知状态开始生命：全零。这个概念只影响类的数据成员，而不影响方法中的局部变量。

## 替换默认构造函数

虽然编译器会自动初始化所有实例变量为零，但对于许多类（可能是大多数类）来说，全零并不是有效状态。考虑本章之前提到的 `BankAccount` 类：

```csharp
public class BankAccount
{
    private int _accountNumber;
    private double _balance;
    // ...其他成员
}
```

虽然初始余额为 0 可能没问题，但账户号码为 0 绝对不是有效银行账户的标志。

在本章的目前阶段，`BankAccount` 类包含了 `InitBankAccount()` 方法来初始化对象。然而，这种方法给使用该类的应用程序软件带来了过多的责任。如果应用程序未能调用 `InitBankAccount()` 方法，银行账户方法可能无法正常工作，这并不是它们的错。

![](img/6df7bb88e9302e98442acc219cfbd7fc_296_1.png)

类不应该依赖像 `InitBankAccount()` 这样的外部方法来使对象处于有效状态。

为了解决这个问题，你可以让你的类提供一个显式的类构造函数，C# 在创建对象时会自动调用它。构造函数本可以命名为 `Init()`、`Start()` 或 `Create()`，但 C# 要求构造函数必须与类名相同。因此，`BankAccount` 类的构造函数所示：

```csharp
public void Main(string[] args)
{
    BankAccount ba = new BankAccount();  // 这调用了构造函数。
}
public class BankAccount
{
    // 银行账户从 1000 开始递增。
    private int _accountNumber;
    private double _balance;
    // ...
}
```

- 5. 在宣布了要动态创建非静态数据成员的意图后，`MyObject` 构造函数使用 `new` 运算符了 `MyOtherObject` 类的对象，并在调用 `MyOtherObject` 构造函数时生成了第二个 `MyOtherObject` 构造消息。
- 6. 控制返回到 `MyObject` 构造函数，然后返回 `Main()`。

做得好！

## 从调试器执行构造函数

从调试器中运行相同的程序非常有启发性：

- 1. 重新生成程序：选择命令 `Build→Build DemonstrateCustomConstructor`。

你还可能需要通过右键点击 `DemonstrateCustomConstructor` 项目并选择“Set As Startup Project”将该项目设置为启动项目。

- 2. 在从调试器开始执行程序之前，在 `MyOtherObject` 构造函数中的 `Console.WriteLine()` 调用处设置一个断点。

要设置断点，点击编辑器窗口左侧的灰色槽，位于你想停止的行行左侧。

图 5-1 显示了我设置断点后的显示：深色圆在槽中。

- 3. 不要选择 `Debug→Start Debugging`，而是选择 `Debug→Step Into`（或按 F11）。

你的菜单、工具栏和窗口应该发生一些变化，然后 `Main()` 函数中的左大括号处会出现亮黄色的高亮。

- 4. 再次按 F11 三次，并将指针轻地悬停在 `localObject` 变量上（不要点击）。

你正要调用 `MyObject` 构造函数。你的显示现在应该像图 5-2 所示。你可以看到 `localObject` 目前在光标下为 `null`。本地（Locals）窗口显示相同的内容。（如果 Locals 窗口可见，选择 `Debug→Windows→Locals` 来显示它。）

![](img/6df7bb88e9302e98442acc219cfbd7fc_299_0.png)

## 图 5-1:

`MyOtherObject` 构造函数中的高亮表示存在断点。

![](img/6df7bb88e9302e98442acc219cfbd7fc_300_0.png)

## 图 5-2:

在你跳入构造函数区域之前，Visual Studio 调试器的显示如所示。

![](img/6df7bb88e9302e98442acc219cfbd7fc_300_1.png)

## 5. 再次按 F11。

程序执行到 `MyOtherObject` 中的断点，如图 5-3 所示的黄色条所示。你是如何到达这里的？`Main()` 中的最后一次调用了 `MyObject` 的构造函数。但在该构造函数开始执行之前，C# 初始化了 `MyObject` 类中的静态数据成员。该数据成员的类型为 `MyOtherObject`，因此初始化它意味着调用它的构造函数——这让你停在了断点处。（如果没有断点，你将不会看到调试器在那里停止，尽管构造函数确实会执行，你可以通过检查构造函数的消息是否显示在控制台窗口来确认这一点。）

## 6. 再次按 F11 两次，你就停在了静态数据成员 `_staticObj` 处，如图 5-4 所示。

你刚刚跳出（step out）的是那个对象的构造函数。

## 7. 在遍历程序时继续按 F11。

当你第一次按 F11 时，你终于停在了 `MyObject` 构造函数的开头。注意，当 `MyObject` 构造函数创建另一个 `MyObject` 数据成员 `_dynamicObj`（非静态的）时，你会第二次进入（step into）`MyOtherObject` 构造函数。

记得继续执行 `Main()` 中的 `Console.Read()` 语句。查看控制窗口后，你可以按 Enter 键关闭它。

![](img/6df7bb88e9302e98442acc219cfbd7fc_301_0.png)

图 5-3: 在进入 `My-Object` 构造函数之前，控制传递给了 `My Other-Object` 构造函数。

![](img/6df7bb88e9302e98442acc219cfbd7fc_301_1.png)

![](img/6df7bb88e9302e98442acc219cfbd7fc_302_0.png)

## 图 5-4: 在执行过 `My-Other-Object` 构造函数后，你回到了构造函数被调用的地方。

第四卷带你彻底介绍了调试器。

## 使用初始化器直接初始化对象

除了允许构造函数中初始化数据成员外，C# 还允许你通过使用初始化器直接初始化数据成员。

因此，我可以这样写 `BankAccount` 类：

```csharp
public class BankAccount
{
    // 银行账户从 1000 开始顺序递增。
    private static int _nextAccountNumber = 1000;
    // 为每个对象维护账号和余额。
    private int _accountNumber = ++_nextAccountNumber;
    private double _balance = 0.0;
    // ... 其他成员 ...
}
```

这就是初始化器的机制。`_accountNumber` 和 `_balance` 在声明时都被分配了值，这与构造函数的效果相同，但不需要在其中执行工作。

清楚具体发生了发生了什么。你可能认为这条语句现在将 `_balance` 设置为 0.0。然而，`_balance` 仅在创建实例时才为 0.0。

新语法要简洁得多：一条语句代替了三条。而且，它简化了无法通过构造函数创建已初始化对象的创建。（我将 `Student` 示例拆分成多行仅仅是为了适应页面宽度——而且这仅仅是因为“Truth or Consequences”这个名字太长了。如果你住在那里，它看起来会更长。）

新的对象初始化语法除了方便之外，并没有给你带来什么特别的额外，但在编码时，便利性是任何程序员清单上的高位因素。简洁性也是如此。此外，当你读到匿名类时，这一特性就变得至关重要。

![](img/6df7bb88e9302e98442acc219cfbd7fc_305_0.png)

请尽情使用新的对象初始化语法吧。我在本书的后续部分也经常使用它。

在“帮助”中查找 *object initializer*（对象初始化器）术语，可以找到关于它适用于哪些类型属性的法律化的语言描述。

![](img/6df7bb88e9302e98442acc219cfbd7fc_305_1.png)

网站上的 `ObjectInitializers` 程序示例演示了对象初始化器。

## 第 6 章：继承：难道就这些吗？

## 本章内容

- 根据另一个更基础的类定义一个类
- 区分 *is a*（是一个）和 *has a*（有一个）
- 用一个类对象替换另一个类对象
- 构建静态或实例成员
- 在继承层次结构中包含构造函数
- 特异地调用基类构造函数

面向对象编程基于四个原则：控制访问的能力（封装）、继承其他类、做出恰当的响应（多态）以及从一个对象间接引用另一个对象（接口）。

继承是一个常见的概念。我是一个人类，除非我刚醒来的时候。我从 `Human`（人类）类继承了某些属性，例如我多或少的交流能力，以及对空气、食物和含有大量咖啡因的碳水饮料的依赖。`Human` 类从 `Mammal`（哺乳动物）类继承了对空气、水和营养的依赖，而 `Mammal` 类继承自 `Animal`（动物）类。

传递属性的能力是非常强大的。你可以利用它以一种经济的方式描述物品。例如，如果我儿子问：“什么是鸭子？”我可以说：“它是一种会嘎嘎叫的鸟。”尽管你可能怎么想，这个答案传达了大量信息。我儿子知道什么是鸟，现在他知道了关于鸭子的所有这些相同特征，加上鸭子额外的属性“嘎嘎叫性”。

面向对象的语言通过允许一个类从另一个类继承属性来表达这种继承关系。这一特性使得面向对象的语言能够生成比不支持继承的语言所生成的模型更接近现实的模型。

## 类继承

在接下来的 `InheritanceExample` 程序中，`SubClass` 类继承自 `BaseClass` 类：

![](img/6df7bb88e9302e98442acc219cfbd7fc_307_0.png)

```csharp
// InheritanceExample -- 提供最简单的
// 继承演示。
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
```
