

# 什么时候用 IS_A，什么时候用 HAS_A 293

需要的。也就是说，SavingsAccount 需要余额，它会向包含的 BankAccount 请求该余额。

在这种情况下，你就说 SavingsAccount **HAS_A**（拥有）一个 BankAccount。硬核面向对象的笑话说，SavingsAccount 组合了（composes）BankAccount。也就是说，SavingsAccount 部分由一个 BankAccount 组成。

# HAS_A 关系

HAS_A 关系在根本上不同于 IS_A 关系。在接下来的应用程序代码段中，这种区别看起来并不糟糕：

```csharp
// 创建一个新的储蓄账户。
BankAccount ba = new BankAccount();
SavingsAccount sa = new SavingsAccount(); // SavingsAccount 的 HAS_A 版本
sa.SavingsAccount(ba, 5);
// 向其存入 100 元。
// 现在积累利息。
sa.AccumulateInterest();
```

问题在于，这个修改过的 SavingsAccount 不能作为 BankAccount 使用，因为它没有继承自 BankAccount。相反，它包含一个 BankAccount —— 这不是同一个概念。例如，这个代码示例：

```csharp
// DirectDeposit - 自动存入我的工资。
void DirectDeposit(BankAccount ba, int pay) {
    ba.Deposit(pay);
}
void SomeMethod() {
    // 下面的示例失败了。
    DirectDeposit(sa, 100);
    continue;
}
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_318_0.png)

Deposit() 不能接受 SavingsAccount 来代替 BankAccount。对于 C# 而言，两者之间不存在明显的联系，因为这里不涉及继承。不过，不要因为这种情况就认为包含是一个坏主意。你只需要以不同的方式处理这个概念才能使用它。

# 什么时候用 IS_A，什么时候用 HAS_A

IS-A 和 HAS_A 关系之间的区别不仅仅是软件便利性的问题。这种关系在现实世界中也有推论。

*

# 294 支持继承的其他特性

例如，福特 Explorer **IS_A**（是一种）汽车（当它是直立的时候）。Explorer **HAS_A**（拥有）一个发动机。如果你的朋友说“开你的车过来”，而你开着 Explorer 出现，他没有理由抱怨。然而，如果你怀里抱着你 Explorer 的发动机出现，他可能就有意见了。（或者至少你看起来是那样）。

Explorer 类应该继承 Car 类，这不仅是为了让 Explorer 能够访问 Car 的方法，也是为了表达两者之间的基本关系。

遗憾的是，初级程序员可能会让 Car 继承自 Motor，这就像给 Car 访问 Motor 的成员一样简单，而 Car 运行恰恰需要这些成员。例如，Car 可以继承 Motor.Go() 方法。然而，这凸显了这种方法的问题：尽管人类在语言中很粗心，但制造汽车并不等同于制造发动机。汽车的“运行”（go）操作完全依赖于发动机，但它们并不是同一个东西 —— 你还需要挂上变速箱挡、释放刹车并完成其他任务。

也许不仅如此，继承自 Motor 误解了事实。汽车根本不是发动机的一种类型。

软件的优雅性本身就是一个值得实现的目标。它增强了可理解性、可靠性和可维护性（并治愈消化不良和痛风）。

硬核面向对象极客为了更简单的程序设计，倾向于使用 HAS_A 而非 IS_A。但在合理的情况下要使用继承，在 BankAccount 层次结构中这可能是合理的。

# 支持继承的其他特性

C# 实现了一组旨在支持继承的特性。我将在接下来的章节中讨论这些特性。

# 可替换类程序程序可以在调用基类对象的地方使用子类。例如，你可能已经在我的某一个示例中见过了。SomeMethod() 可以将 SavingsAccount 对象传递给 DirectDeposit() 方法，而该方法期望一个 BankAccount 对象。

你可以让这种转换更加显式：

```csharp
BankAccount ba;
SavingsAccount sa = new SavingsAccount(); // 原始的，不是 SavingsAccount
// 或者；
ba = sa; // 隐式地将子类转换为基类。
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_319_0.png)

# 支持继承的其他特性 295

```csharp
ba = (BankAccount)sa; // 但倾向于显式转换。
// 不可以；
s = ba;
s = (SavingsAccount)ba; // 错误：隐式将基类转换为子类
// 然而，允许显式转换。
```

第一行将一个 SavingsAccount 对象赋值给 BankAccount 变量。C# 为你转换了对象。第二行使用强制转换显式地转换对象。

最后两行尝试将 BankAccount 对象转换回 SavingsAccount。你可以完成此操作，但 C# 不会为你完成。这就像是将较大的数值类型（如 double）转换为较小的类型（如 float）。C# 没有实现它，因为该过程涉及数据丢失。

IS-A 属性不是自反的。也就是说，即使一个 Explorer 是一辆汽车，汽车也不一定是 Explorer。同样，BankAccount 不一定是 SavingsAccount，因此不允许隐式转换。最后一行是允许的，因为程序员表达了愿意“放手一”。她一定知道些什么。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_320_0.png)

# 运行时的无效情况

通常，将对象从 BankAccount 转换为 SavingsAccount 是一个危险的操作。考虑这个示例：

```csharp
public static void ProcessAmount(BankAccount bankAccount)

// 向账户存入大额。
bankAccount.Deposit(10000.0M);
// 如果对象是 SavingsAccount，现在收集利息。
SavingsAccount savingsAccount = (SavingsAccount)bankAccount;
savingsAccount.AccumulateInterest();

public static void TestCast()
{
```

```csharp
SavingsAccount sa = new SavingsAccount();
ProcessAmount(sa);
BankAccount ba = new BankAccount();
ProcessAmount(ba);
}
```

ProcessAmount() 执行了几个操作，调用了 AccumulateInterest() 方法。将 ba 强制转换为 SavingsAccount 是必要的，因为 bankAccount 参数被声明为 BankAccount。程序正常编译，因为所有类型转换都是通过显式转换完成的。

TestCast() 第一次调用 ProcessAmount() 时一切顺利。SavingsAccount 对象 sa 被传递给 ProcessAmount() 方法。从 BankAccount 到 SavingsAccount 的转换没有产生问题，因为 ba 对象本初就是 SavingsAccount。

| 第二卷第 6 章 | 我得到了什么？ | 继承：那是 |
| --- | --- | --- |

# 296 支持继承的其他特性

然而，第二次调用 ProcessAmount() 并不幸运。转换为 SavingsAccount 是不允许的。ba 对象没有 AccumulateInterest() 方法。

错误的转换会在程序执行期间产生错误（运行时错误）。运行时错误比编译错误更难发现和修复。糟糕的是，它们可能发生在你其他用户身上，而他们并不理解。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_321_0.png)

# 使用 is 运算符避免转换

如果 ProcessAmount() 方法能够在转换之前确保传递给它的对象是 SavingsAccount，它就能工作。C 提供了两个用于此目的关键字：is 和 as。

is 运算符接受左侧的操作。如果左侧对象的运行时类型与右侧类型兼容，运算符返回真。在尝试强制转换之前使用它来验证转换是否合法。

可以通过运算符修改之前的章节以避免运行时错误：

```csharp
public static void ProcessAmount(BankAccount bankAccount)
{
// 向账户存入大额。
bankAccount.Deposit(10000);
// 如果对象是 SavingsAccount . . .
if (bankAccount is SavingsAccount)
{
    // 然后现在收集利息（保证转换成功）。
    SavingsAccount sa = (SavingsAccount)bankAccount;
    sa.AccumulateInterest();
}
// 否则，你不进行转换 —— 但为什么 BankAccount 不是
// 你预期的那样？这可能是一个错误情况。
}
```

