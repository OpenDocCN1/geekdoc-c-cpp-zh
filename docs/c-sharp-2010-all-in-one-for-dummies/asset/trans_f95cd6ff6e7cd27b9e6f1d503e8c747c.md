
在使用中，这些属性的表现形式如下：

```csharp
BankAccount ba = new BankAccount();
// Set the account number property.
ba.AccountNumber = 123;
// Get both properties.
Console.WriteLine("{0} {1} {2}", ba.AccountNumber, ba.Balance);
```

AccountNumber 和 Balance 属性无论在外观还是使用上，都非常类似于公共数据成员。然而，属性使类能够保护内部成员（Balance 是只读属性）并隐藏其实现（底层 _balance 数据成员是私有的）。请注意，Balance 执行了一次转换——它本可以执行任意数量的计算。属性不一定是单行代码。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_296_0.png)

按照约定，属性名以大写字母开头。请注意，属性没有括号：是 Balance，而不是 Balance()。

属性并不一定效率低下。C# 编译器可以将简单的访问器优化到与直接访问数据成员生成同样多机器代码的程度。这个概念不仅对 C# 本身很重要。C# 库中到处都使用了属性，你也应当这样做。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_296_1.png)

*即使是同一类中的方法，也应使用属性来访问类的数据成员。*

## 静态属性

静态（类）数据成员可以通过静态属性公开，如下面的简化示例所示（注意其紧凑的布局）：

```csharp
public class BankAccount
{
    private static int _nextAccountNumber = 1000;
    public static int NextAccountNumber { get { return _nextAccountNumber; } }
    // ...
}
```

NextAccountNumber 属性通过类访问，如下所示，因为它不是实例属性（它被声明为 static）：

```csharp
// Read the account number property.
int value = BankAccount.NextAccountNumber;
```

（在此示例中，value 处于属性的上下文之外，因此它不是保留字。）

## 带副作用的属性

get 操作除了简单检索关联属性外，还可以执行额外的工作，如下所示：

```csharp
public static int AccountNumber
{
    // Retrieve the property and set it up for the
    // next retrieval by incrementing it.
    get { return ++_nextAccountNumber; }
}
```

该属性在返回结果之前会递增静态账号成员。然而，这可能不是一个好主意，因为属性的使用者除了实际读取属性外，不会得到任何正在发生其他事情的提示。这种递增就是一种副作用。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_297_0.png)

与它们模仿的访问器方法一样，属性除了设置数据成员的值之外，不应改变类的状态。属性和方法通常都应避免副作用，因为它们可能导致难以察觉的 bug。应尽可能直接、明确地更改类。

## 新特性：让编译器为您编写属性

上一节中描述的大多数属性都是完全例行的，编写它们很繁琐（虽然简单）：

```csharp
private string _name; // An underlying data member for the property
public string Name { get { return _name; } set { _name = value; } }
```

因为您反复编写同样的样板代码，所以 C# 3.0 编译器现在为您代劳了。对于前面的属性（包括私有数据成员），您只需编写这一行：

```csharp
public string Name { get; set; }
```

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_297_1.png)

这一行大致相当于

```csharp
private string <comename>; // What's <comename>? Don't know or care.
public string Name { get { return <comename>; } set { <comename> = value; } }
```

编译器会创建一个无名数据成员以及访问器样板代码。csharp102.info 上的 AccessorProperty Shortcuts 示例演示了这种用法。这种风格鼓励甚至在其包含类的其他成员中也使用该属性，因为您只知道属性名。因此，您必须同时具备 get 和 set。您可以使用属性语法初始化此类属性。

```csharp
public int AnInt { get; set; } // Compiler provides a private variable.

AnInt = 2; // Initialize compiler-written instance variable via property.
```

## 具有访问级别的访问器

访问器属性不一定非要声明为 public。您可以在任何适当的级别声明它们，甚至可以是 private，只要该访问器仅在其类内部使用。（接下来的示例将 Name 属性标记为 internal。）

您甚至可以单独调整访问器的 get 和 set 部分的访问级别。假设您不想在类外部公开 set 访问器——它仅供内部使用。您可以这样编写属性：

```csharp
internal string Name { get; private set; }
```

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_298_0.png)

csharptwo.info 上的 AccessorPropertyShortcuts 示例演示了这种用法。

## 让对象有一个良好的开端——构造函数

控制类访问只是问题的一半：对象要想成长，就需要有一个良好的人生开端。类可以提供应用程序调用的初始化方法来启动事务，但应用程序可能会忘记调用该方法。类以垃圾数据开始，之后情况也不会好转。如果你想让类负起责任，就必须确保它有机会正确地开始。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_298_1.png)

C# 通过为您调用初始化方法来解决这个问题——例如：

```csharp
MyObject mo = new MyObject();
```

换句话说，这条语句不仅从特殊内存区域获取对象，还初始化该对象的成员。

请将类和对象这两个术语区分开来。Cat 是一个类。我的猫 Striper 是 Cat 类的一个对象。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_298_2.png)

第 II 册 第 5 章 让类负起责任

该程序定义了一个类 MyObject，其中包含一个 int 类型的简单数据成员 n 和一个对象引用 nextObject（两者都声明为 internal）。Main() 方法创建一个 MyObject，然后显示 n 和 nextObject 的初始内容。

执行该程序的输出如下所示：

```
localObject.n is 0
localObject.nextObject is null
Press Enter to terminate...
```

创建对象时，C# 会执行编译器提供的一小段代码来初始化对象及其成员。如果不做任何处理，数据成员 localObject.n 和 nextObject 将包含随机的垃圾值。

在创建时初始化值的代码是默认构造函数。它“构造”类，即初始化其成员。因此，C# 确保对象在已知状态下开始生命周期：全为零。这个概念只影响类的数据成员，不影响方法中的局部变量。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_300_0.png)

### 替换默认构造函数

尽管编译器会自动将所有实例变量初始化为零，但对于许多类（可能是大多数类）来说，全零并不是有效状态。考虑本章前面提到的以下 BankAccount 类：

```csharp
public class BankAccount
{
    private int _accountNumber;
    private double _balance;
    // ... other members
}
```

虽然 0 的初始余额可能没问题，但 0 的账号绝对不是有效银行账户的标志。

在本章的这个阶段，BankAccount 类包含 InitBankAccount() 方法来初始化对象。然而，这种方法将过多的责任放在了使用该类的应用程序软件上。如果应用程序未能调用 InitBankAccount() 方法，银行账户方法可能无法工作，而这并非它们自身的过错。

类不应依赖诸如 InitBankAccount() 之类的外部方法来使对象以有效状态启动。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_300_1.png)

第 II 册 第 5 章 让类负起责任
