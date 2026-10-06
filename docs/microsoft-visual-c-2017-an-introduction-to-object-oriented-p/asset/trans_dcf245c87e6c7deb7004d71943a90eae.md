

```c
using static System.Console;
delegate void GreetHandler(string s);
class Greeting {
    public static void Hello(string s)
    {
        WriteLine("Hello, {0}", s);
    }
    public static void Goodbye(string s)
    {
        WriteLine("Goodbye, {0}", s);
    }
    static void Main()
    {
        GreetingHandler firstDel, secondDel;
        firstDel = new GreetHandler(Hello);
        secondDel = new GreetHandler(Goodbye);
        GreetMethod(firstDel, "Cathy");
        GreetMethod(secondDel, "Bob");
    }
    public static void GreetMethod(GreetingHandler gd,
        string name)
    {
        WriteLine("The greeting is:");
        gd(name);
    }
}
```

图 13-6 问候程序

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_630_0.png)

图 13-7 问候程序的输出

委托的用处在于方法引用可以传递给另一个方法，因此接收方法可以是自定义的。通过 C# 的许多其他特性（以及所有其他编程语言），你可以使用其他技术来实现相同的结果。例如，你可以乐意地使用其他技术产生如 Hello, Cathy 的简单输出。然而，你在这里学习关于委托的少量知识，因为你将在在本章稍后的部分看到，它们被用于 C# GUI 环境中响应事件的代码中。

## 创建组合委托

你可以使用 `=` 运算符将一个委托赋值给另一个。你还可以使用 `+` 和 `-=` 运算符将委托组合成组合委托，该委托会调用构建它的各个委托。例如，假设你有名为 `del11`、`del12` 和 `del13` 的委托，并将方法 `M1()` 的引用赋值给 `del11`，将方法 `M2()` 的引用赋值给 `del12`。当执行语句 `del13 = del11 + del12` 时，它变成了一个顺序执行 `M1()` 和 `M2()` 的委托。只有具有相同参数列表的委托才能组合，且委托必须具有 `void` 返回类型。此外，你可以使用 `-` 和 `-=` 运算符从组合委托中移除委托。组合委托是委托的集合，`+=` 和 `-=` 运算符用于从集合中添加和删除项。

图 13-8 显示了一个包含组合委托的程序。该程序与图 13-6 中的 Greet 程序相比有两个变化：类名（`Greeting2`）以及创建组合委托的阴影语句。委托 `firstDel` 现在执行两个方法：`Hello()` 和 `Goodbye()`，而 `secondDel` 仍然执行 `Goodbye()`。
图 13-9 显示了它的输出：Cathy 使用了两个方法，而 Bob 仅使用了一个。

```c
using static System.Console;
delegate void Greeting(string s);
class Greeting2
{
    public static void Hello(string s)
    {
        WriteLine("Hello, {0}!", s);
    }
    public static void Goodbye(string s)
    {
        WriteLine("Goodbye, {0}!", s);
    }
    public static void Main()
    {
        GreetingHandler firstDel = new GreetingHandler(Hello);
        secondDel = new GreetingHandler(Goodbye);
        firstDel += secondDel;
        GreetMethod(firstDel, "Cathy");
        GreetMethod(secondDel, "Bob");
    }
    public static void GreetMethod(GreetingHandler gd, string name)
    {
        WriteLine("The greeting is:{0}");
        gd(name);
    }
}
```

**图 13-8** Greeting2 程序

## 第 13 章 处理事件

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_632_0.png)

**图 13-9** Greeting2 程序的输出

观看视频 *事件处理 (Event Handling)*。

##两个真理一个谎言
理解委托

- 1. 委托是一个包含方法引用的对象。
- 2. 一旦创建了委托，它可以封装任何与委托具有相同标识符的方法。
- 3. 可以使用 `+=` 运算符创建组合委托；它会调用构建它的委托。

> 虚假语句是 #2。一旦你创建了委托，返回类型和参数列表必须与委托匹配。它可以进行封装。

## 你来做

创建委托
为了演示委托的工作原理，你将在接下来的步骤中创建两个委托实例并为它们分配不同的方法引用。

- 1. 打开一个名为 **DiscountDelegateDemo** 的新控制台项目。使用 `using` 编写必要的代码，然后创建一个封装接受 `double` 参数的 `void` 方法的委托：

```c
using System;
using System.Console;
delegate void DiscountHandler(ref double saleAmount);
(继续)
```

- 2. 开始创建一个 `DiscountDelegateDemo` 类，其中包含一个 `StandardDiscount()` 方法。该方法接受一个代表销售金额的引用参数。如果销售金额至少为 $1,000，则计算 5% 的折扣并从销售金额中减除。如果销售金额小于 $1,000，则不进行任何减除。

```c
class DiscountDelegateDemo {
    public static void StandardDiscount(ref double saleAmount) {
        const double DISCOUNT_RATE = 0.05;
        const double CUTOFF = 1000.00;
        double discount;
        if(saleAmount >= CUTOFF) {
            discount = saleAmount * DISCOUNT_RATE;
        } else {
            discount = 0;
        }
        saleAmount -= discount;
    }
}
```

- 3. 添加一个 `PreferredDiscount()` 方法。该方法接受一个代表销售金额的引用，并对每次销售计算 10% 的折扣。

```csharp
public static void PreferredDiscount(ref double saleAmount) {
    const double SPECIAL_DISCOUNT = 0.10;
    double discount = saleAmount * SPECIAL_DISCOUNT;
    saleAmount -= discount;
}
```

- 4. 添加一个 `Main()` 方法，声明由用户提供的变量（销售金额和代码）。声明两个 `DiscountHandler` 委托对象。将 `StandardDiscount()` 方法赋值给其中一个，将 `PreferredDiscount()` 方法赋值给另一个。

```csharp
static void Main() {
    double saleAmount;
    char code;
    DiscountHandler firstDel, secondDel;
    firstDel = new DiscountHandler(StandardDiscount);
    secondDel = new DiscountHandler(PreferredDiscount);
    Write("Enter amount of sale ");
    saleAmount = Convert.ToDouble(ReadLine());
    Write("S for standard discount, " +
      "P for preferred discount");
    code = Convert.ToChar(ReadLine());
    if(code == 'S')
        firstDel(ref saleAmount);
    else
        secondDel(ref saleAmount);
    WriteLine("New sale amount is {0}", saleAmount.ToString("C2"));
}
```

- 5. 保存文件，然后编译并执行。图 13-10 显示了程序多次执行时的结果。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_634_0.png)

图 13-10 Discount程序的程序的示例

当你组合委托时，可以使用一个语句调用多个方法。在接下来的步骤中，你创建一个组合委托来演示组合的工作原理。

- 打开 `DiscountDelegateDemo` 文件，并立即将其保存为 `DiscountDelegateDemo`。
- 在 `Main()` 方法中，在声明现有版本的语句中添加第三个委托对象，如下：
`DiscountHandler firstDel, secondDel, thirdDel;`
- 在为现有委托对象赋值的语句之后，添加将 `firstDel` 对象赋值给 `thirdDel` 的语句，然后将其 `secondDel` 组合。
`thirdDel = firstDel;`
`thirdDel += secondDel;`
- 修改代码提示如下所示，以反映三个选项。标准和优惠折扣保持不变，但极端折扣（假设为特殊客户提供）提供了两种折扣：首先对任何大于或等于 $1,000 的销售额减去 5%，然后额外提供 10% 的折扣。
- 修改 `if` 语句，如果用户没有输入 S 或 P，则应用极端折扣。

```csharp
Write("Enter S for standard discount, " + 
  "P for preferred discount," + 
  "\nX for extreme discount\");
```

```csharp
if(code == 'S')
  firstDel(ref saleAmount);
else
  if(code == 'P')
    secondDel(ref saleAmount);
  else
    thirdDel(ref saleAmount);
```

