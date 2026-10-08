
```csharp
public sealed class Director : Employee
{
    public Director(string firstName, string lastName, int monthly)
    : base(firstName, lastName, "Director", monthly) {}
}
```

# 注释

继承并不是一个特别困难的概念——至少当你见过几次之后是这样的——但有些事情是你必须注意的：

- 类（Class）——例如 `Employee` 可能有一个或多个派生类，但一个类只能继承一个类。
- 多态（Polymorphism）——运行时系统记住对象的特定类型（在创建新对象时使用的类型是面向对象编程最重要的概念之一）。

此外，还有一些与继承相关的名称，理解它们很重要：

- `base`
- `protected`
- `virtual`
- `override`

你可以在上面的示例看到这些词是如何使用的。

# 12 Object 类

我上面在 `Coin`、`Dice`、`Cup` 等类中看到过，这些类显然没有使用继承——表面上如此，但实际上它们间接继承了 `Object` 类。如果你不写任何内容，该类会自动继承这个类，而且所有类无例外地直接或间接继承 `Object`。事实远不止于，对于任何类型，无论是值类型还是引用类型，都是如此。

C# 定义了 `System.Object` 的别名类，这是一个保留字，就像 `string` 是 `System.String` 类的别名完全一样。

`Object` 类包含的内容不多，但它的主要用途是作为所有类型的基类。它定义了一些我将提到的方法：`ToString()`，它返回对象的字符串表示。考虑以下内容：

```csharp
class ZipCode
{
    private string code;
    private string name;
}
```

![](img/f84352ec481fd05dc2bc853aa8989838_108_0.png)

## C# 1 编程入门与 C# 语言

```csharp
class ZipCode
{
    public ZipCode(string code, string name)
    {
        this.code = code;
        this.name = name;
    }

    public string code
    {
        get { return code; }
    }

    public string name
    {
        get { return name; }
    }

    public override string ToString()
    {
        return code + " " + name;
    }

    public override bool Equals(object obj)
    {
        if (obj is ZipCode)
        {
            ZipCode z = (ZipCode)obj;
            return code.Equals(z.code) && name.Equals(z.name);
        }
        return false;
    }
}
```

如果你想测试这个，可以这样做：

```csharp
static void Test1()
{
    ZipCode z1 = new ZipCode("7800", "Skive");
    ZipCode z2 = new ZipCode("7800", "Skive");
    Console.WriteLine(z1.Equals(z2));
}
```

当你运行该方法，你将得到结果：

![](img/f84352ec481fd05dc2bc853aa8989838_109_0.png)

## C# 1 编程入门与 C# 语言

我将提到 `Object` 类中的另一个方法 `GetHashCode()`。它是一个返回整数的方法，该整数可以被视为代码标识。通常它是根据对象的引用确定的，但与 `ToString()` 和 `Equals()` 一样，由程序员来重写该方法，如果需要根据对象的值返回代码。

考虑以下方法，你应该特别注意该方法有一个对象作为参数：

```csharp
static void Print(object obj)
{
    Console.WriteLine(obj.GetType());
    Console.WriteLine(obj.GetHashCode());
    Console.WriteLine(obj);
}
```

# C# 编程与 C# 语言简介

你还应该注意 `GetType()` 方法，它是 `Object` 类中的方法，在此情况下，它用于打印对象的类型名称。下面的方法创建一个 `object` 类型的数组并在控制台上打印其元素：

```csharp
static void Test3() {
    object[] t = { 23, 3.14, "Volmer", new Postnummer("7800", "Skive") };
    for (int i = 0; i < t.Length; i++) Print(t[i]);
}
```

如果你运行该方法，将得到以下结果：

![](img/f84352ec481fd05dc2bc853aa8989838_111_0.png)

你应该主要注意两点：

- 作为形式参数对象的方法，可能具有任何类型的实际参数
- 类型为 `object` 的数组可以包含任何内容，无论类型如何

乍一看这听起来很聪明，但你应该意识到，这意味着编译器无法检查，因此基于 `object` 类型的代码很容易包含错误。

上述关于 `Object` 类的示例被称为 Exam28。

# C# 1 编程与 C# 语言简介

## 13 抽象类

在本章中，我将介绍抽象类的概念。它是一种无法实例化的类——你不能创建抽象类的对象，但抽象类可以作为其他具体类的基类。

Exam32

### 抽象点

我将再次从一个示例开始，目的是展示语法，该示例与 Exam31 基本相同。现在 `Point` 类是抽象的了：

```csharp
public abstract class Point
{
    private int x;
    private int y;

    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}
```

![](img/f84352ec481fd05dc2bc853aa8989838_112_0.png)

# C# 1 编程与 C# 语言简介

## 抽象类

```csharp
public int X
{
    get { return x; }
    set { x = value; }
}

public int Y
{
    get { return y; }
    set { y = value; }
}

public override string ToString()
{
    return string.Format("{0}, {1}", x, y);
}

public abstract void Dec();
public abstract void Inc();
```

有两个区别。该类有两个抽象方法 `Dec()` 和 `Inc()`。这些方法没有代码，仅仅是定义。这意味着使用 `Point` 类的人知道这些方法存在，但不知道它们是如何工作的的。第二个区别是该类被定义为抽象的。它必须如此，这意味着该类不能被实例化——你不能创建 `Point` 类型的对象。

`NewPoint` 类继承自 `Point`，因此必须实现这两个抽象方法，所以它们是执行某些操作的具体方法：

```csharp
public class NewPoint : Point
{
    public NewPoint(int x, int y) : base(x, y) { }
}

public override void Dec()
{
    --X;
    --Y;
}

public override void Inc()
{
    ++X;
    ++Y;
}
```

注意，在派生类中实现的抽象方法前面必须带有 `override` 关键字。

# C# 1 编程与 C# 语言简介

下面是一个使用 `NewPoint` 类的 `Main()` 方法：

```csharp
static void Main(string[] args)
{
    Point p = new NewPoint(2, 3);
    Console.WriteLine(p);
    p.Inc();
    Console.WriteLine(p);
    p.Dec();
    Console.WriteLine(p);
}
```

![](img/f84352ec481fd05dc2bc853aa8989838_114_0.png)

`p` 是一个 `NewPoint` 对象，但在程序中被定义为 `Point`。这是可能的，因为 `NewPoint` 专门是一个 `Point`，但你应该特别注意，即使 `p` 是一个 `Point`，你仍然可以写

`p.Inc();`

由于 `Point` 有一个抽象方法 `Inc()`，编译器知道 `Point` 对象拥有这样一个方法（尽管它是在派生类中定义的），因此上述语句是有意义的。

### 贷款

作为一个示例，我将编写一个可以代表银行贷款的类。贷款（在本示例中）的特征是本金、期数和利率。我假设利率在整个还款期内保持不变，并且每期在到期日还款一次，且还款在贷款启动后一期发生。我还假设你对以下信息感兴趣

- 第 n 次还款
- 第 n 次还款时的还款金额
- 第 n 次还款时的利息
- 第 n 次还款后的余额

完成后的程序必须打印一份贷款摊还计划，该计划是每个账期结束后贷款情况的概述。

# C# 1 编程与 C# 语言简介

## 抽象类

### 如何实现

对应此贷款可以用以下类表示：

| 本金 | double |
| 利率 | double |
| 期数 | int |
| 本金 | double |
| 利率 | double |
| 期数 | int |
| 还款(n) | double |
| 利息(n) | double |
| 还款金额(n) | double |
| 余额(n) | double |

现在有多种类型的贷款，作为一个示例，你有一种随时间减少的等本贷款。对于等额贷款，你每次必须支付相同的金额。

![](img/f84352ec481fd05dc2bc853aa8989838_115_0.png)

# C# 1 编程与 C# 语言简介

## 抽象类

你也可以查看等额贷款，其特征是还款金额在整个期间保持不变。这意味着利息和还款之间的关系通过以下公式表示：

```csharp
payment = principal * rate / (1 - (1 + rate)^-periods)
```

最后，第 n 期还款后的剩余余额计算如下：

```c
outstanding = principal * ((1 + rate)^n - 1) / ((1 + rate)^periods - 1)
```

如果你观察上面的 `Loan` 类，发现需要两个版本：自然会考虑一个共同的基类两个类：等本贷款和等额贷款。当两个类有许多共同点时，自然会考虑一个共同的基类和两个派生类：

```csharp
public abstract class Loan {
  protected double principal;
  protected double rate;
  protected int periods;
}
```

# C# 1 编程基础与 C# 语言介绍

## 抽象类

```csharp
public override double Payment(int n)
{
    return principal * rate / (1 - Math.Pow(1 + rate, -periods));
}
public override double Outstanding(int n)
{
    return principal * Math.Pow(1 + rate, n) - Payment(0) *
    (Math.Pow(1 + rate, n) - 1) / rate;
}
public override double Interest(int n)
{
    return Outstanding(n - 1) * rate;
}
public override double Repayment(int n)
{
    return Payment(n) - Interest(n);
}
```

程序必须打印一份贷款还款计划，这是一张显示每次还款贷款状态的表格：

```csharp
public class Amortization
{
    private Loan loan;
```

![](img/f84352ec481fd05dc2bc853aa8989838_118_0.png)

# C# 编程基础与 C# 语言介绍

## 抽象类

```csharp
public Amortisation(Loan loan)
{
    this.loan = loan;
}

public void Print()
{
    Console.WriteLine("Principal: {0, 10:F}", loan.Principal);
    Console.WriteLine("Rate of interest: {0, 10:F}", loan.Rate);
    Console.WriteLine("Number of periods: {0, 10:D}\n", loan.Periods);
    Console.WriteLine("\nPeriods Payment Repayment Outstanding");
    for (int n = 1; n <= loan.Periods; n++)
    {
        Console.WriteLine("{0,0} {1,15:F} {2,15:F} {3,15:F} {4,15:F}", n, loan.Payment(n), loan.Repayment(n), loan.Interest(n), loan.Outstanding(n));
    }
}
```

# 解析

请注意，`Loan` 类被定义为抽象类。这可能是因为它包含了抽象方法。抽象方法是一种没有定义体的方法——即没有编写具体实现。在这种情况下，有四个抽象方法。抽象方法关于如何计算付款取决于它指的是哪种贷款。只有当你知道正在处理的是哪种贷款时，才能实现该方法。抽象类仅仅是一个原型定义，其中方法通过其名称、返回类型和参数进行定义，但缺少了方法体。

`Loan` 是一个类型，尽管它是抽象的，但你不能创建 `Loan` 类型的对象，该类型可以作为方法的参数类型使用。任何被告知正在处理 `Loan` 类型对象的人都知道它具有三个属性（以及对应的方法，如 `Payment()` 等），并且如果这四个抽象方法存在，你就可以使用它们。

`SerialLoan` 类继承自 `Loan`，因此由 `SerialLoan` 类负责实现这四个抽象方法，因为 `SerialLoan` 拥有所需的知识——这些知识在 `Loan` 类中是未知的。抽象方法的实现是虚拟的（virtual），但 `SerialLoan` 明确是一个 `Loan`。

`AnnuityLoan` 类也容易实现，它仅需在 C# 中编写公式即可。这里你应该注意 `Pow()` 方法，它是 `Math` 类的一个静态方法，用于计算参数的幂。

最后是 `Amortisation`，它可以打印贷款的还款计划。这里你应该注意该类有一个类型为 `Loan` 的实例变量，该变量在构造函数中初始化。因此你可以有一个类型为抽象类的变量，因为 `SerialLoan` 和 `AnnuityLoan` 的具体对象也是 `Loan` 类型。请注意，`Amortisation` 类对具体的贷款类型一无所知，但尽管如此，只要它们继承自 `Loan` 类，就可以编写该类的方法。

# C# 1 编程基础与 C# 语言介绍

## 抽象类

# 测试

如果你使用以下程序测试上述类：

```csharp
class Program
{
    static void Main(string[] args)
    {
        Amortisation table1 = new Amortisation(new SerialLoan(10000, 0.02));
        Amortisation table2 = new Amortisation(new AnnuityLoan(10000, 0.02));
        table1.Print();
        table2.Print();
    }
}
```

你将如下结果：

![](img/f84352ec481fd05dc2bc853aa8989838_120_0.png)

### 类

在最后的示例中，通常有多个类以及 `Main` 程序。在所有示例中，类代码都在同一个文件中，但随着示例变得复杂，为了清晰起见，将每个类放在自己的文件中是一种可行策略，这更容易理解。

# 注释

特别注意，类可以是抽象的，尽管它有抽象方法。这可以确保一个类不能被实例化。

## 14 接口

抽象类可以包含类所拥的所有内容，即变量、构造函数、方法等。某些方法可以是抽象的，这对应于具体的类。相比之下，接口是一种只包含抽象方法的类型。

## 33

## 再次介绍接口

以下是 `IPoint`：
