
```
// In assembly InternalLimitsAccess:
class Congress
{
    static void Main(...)
    {
        // Code to oversee CIA
    }
}

// In assembly CIAAssembly:
public class GroupA
{
    private string _secretFormulaForCocaCola; // Secret X
}
public class GroupB
{
    public void DoSomethingWithSecretX()
    {
        // Do something with Secret X, if only you could access it.
    }
}
```

现在 GroupB 看不到秘密 X，但假设它确实有正当理由需要知道秘密 X。当然，GroupA 可以把秘密 X 提升为 public 状态，但一旦这样做，这个秘密就不再那么秘密了。如果 GroupB 能看到这个秘密，那么国会里那些爱窥探的人也能看到。更糟的是，CNN 也会知道，更不用说 Fox、ABC 和其他电视网了。你也知道那些人保守秘密的本事如何。哦，对了——俄罗斯也能看到秘密 X。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_413_0.png)

幸运的是，C# 还有 internal 关键字。使用 internal 只是比 public 低一级，但远高于 private。如果你改为用 internal 关键字标记 GroupA 类及其“public”方法——即在类外部可见的方法——那么 CIA 的每个人都能看到并访问秘密 X——只要你把秘密本身（一个数据成员）标记为 internal，或者提供一个 internal 属性来获取它，如下面这个版本所示：

```
// In assembly CIAAssembly:
internal class GroupA
{
    private string _secretFormulaForCocaCola; // Secret X
    internal string SecretX { get { return _secretFormulaForCocaCola; } }
}
public class GroupB
{
    public void DoSomethingWithSecretX()
    {
        // Do something with Secret X, now that we can see it:
        Console.WriteLine("I know Secret X, which is {0} characters long, but " +
            "I'm not telling.", GroupA.SecretX.Length);
    }
}
```

现在 GroupB 类拥有了它所需的访问权限——而且它不会交出这个秘密（即使受到水刑威胁）。它在 Main() 中告诉 Congress 的全部内容只是：它知道秘密 X，并且秘密 X 有 11 个字符。下面是那段代码：

```csharp
class Congress
{
    static void Main(string[] args)
    {
        // Code to oversee CIA
        // The following line doesn't compile because GroupA isn't accessible
        // Outside CIAAssembly. Congress can't get at GroupA over at CIA.

        // CIAAssembly.GroupA groupA = new CIAAssembly.GroupA();

        // Class Congress can access GroupB because it's declared public.
        // GroupB is willing to admit to knowing the secret, but it's
        // not telling — except for a small hint.
        GroupB groupB = new GroupB();
        groupB.DoSomethingWithSecretX();

        // Wait for user to acknowledge results.
        Console.WriteLine("Press Enter to terminate...");
        Console.Read();
    }
}
```

从 Main() 来看，GroupA 现在不可见，因此尝试构造它的实例无法通过编译。但由于 GroupB 是 public，Main() 可以访问它并调用其 public 方法 DoSomethingWithSecretX()。

等等！我很高兴地报告，CIA 确实必须就某些话题与国会沟通——但当然是在“需要知道”的基础上，仅限于部分国会议员和参议员。他们只要出示适当的凭据，就已经可以通过 GroupB 做到这一点，不过你需要把这些凭据加入代码：

```csharp
public string DoSomethingWithSecretXUsingCredentials(string credentials)
{
    if (credentials == "congressman with approved access")
    {
        return GroupA.SecretX;
    }
    return string.Empty;
}
```

internal 关键字使类及其成员只能在其自身程序集内部访问。但在该程序集内部，internal 项对所有本地类实际上都是“public”。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_414_0.png)

不过，有时基类并不会提供这类访问方法供其子类（以及其他代码）使用。如果 BankAccount 中的 _balance 数据成员是 private，并且该类不提供 Balance 属性，那该怎么办？

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_416_0.png)

轮到 protected 关键字登场了：如果基类中的 _balance 实例变量声明为 protected 而不是 private，外部代码就看不到它——对外部代码而言它实际上就是 private。但子类可以正常看到它。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_416_1.png)

更好的解决方案是像之前一样在 BankAccount 中把 _balance 标记为 private，然后提供一个标记为 protected 的 Balance 属性。SavingsAccount 等子类可以通过 Balance 属性访问 _balance。但余额对外部代码不可见，这甚至能对子类保护 BankAccount 的实现。

## 第二部
### 第 10 章
## 我可以在库中使用你的命名空间吗？

如果余额确实需要让外部代码访问（只读），那么当然应该提供 public 的 Balance 属性来获取余额（只读）。然而，你可能仍然需要从 SavingsAccount 内部设置余额。为此，可以给 Balance 的 set 访问器 protected 访问权限——可从 SavingsAccount 和其他子类访问，但外部代码不可访问。本迷你书第 5 章关于属性的讨论展示了如何做到这一点，代码如下所示：

```
// In BankAccount:
public decimal Balance
{
    get { return _balance; }        // Public
    protected set { _balance = value; }  // Not public
}
```

Web 上的 ProtectedLimitsAccess 示例演示了刚才描述的 protected 关键字用法。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_416_2.png)

你甚至可以在另一个程序集中子类化 BankAccount，而该子类可以访问 BankAccount 中声明为 protected 的任何内容。ProtectedLimitsAccess 示例也演示了这一过程。

该示例有两个 BankAccount 的子类：一个与 BankAccount 位于同一程序集，另一个位于不同程序集。关于 protected 的有趣之处在于，两个 BankAccount 子类中的任何一个都能访问 BankAccount 中标记为 protected 的任何项。子类不必与其基类位于同一程序集。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_416_3.png)

能够从基类所在程序集之外扩展（子类化）一个类，会对安全性产生影响，这就是为什么许多类应标记为 sealed。密封一个类可以防止外部代码通过子类化它来获得访问权限。因此，建议只在类需要可子类化时才使其可扩展（非密封）。让同一程序集中的其他代码访问基类成员——包括同一程序集中的子类——的一种方法是把这些成员标记为 internal 而不是 protected。这样，你就能让本地子类获得所需的访问级别，同时阻止外部子类访问。当然，程序集中的其他类随后也被允许访问。这个方案可能并不理想，但如果安全性是需要考虑的因素，它应该更安全。

## protected internal：更慷慨的保护者

把 BankAccount 基类中的项设为 protected internal，而不只是 protected，只是为这些项在程序中的可访问性增加了一个新维度。单独使用 protected 允许子类（程序中的任何程序集）访问基类中的受保护项。加上 internal 则把这些项的可访问性扩展到任何类，只要该类与 BankAccount 位于同一程序集，或者至少是其他程序集中的子类。

在 csharp102.info 上的 ProtectedInternalLimitsAccess 示例中，你可以看到这种效果。定义在 BankAccount 自身程序集中的 AnotherClass 类可以访问 Balance 属性中的 protected internal set 访问器。然而，另一个程序集中几乎相同的 Another Class 类无法访问 Balance 的 set 访问器来设置余额。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_417_0.png)

让项尽可能不可访问。从 private 开始。如果你的某些代码需要更多访问权限，再有选择地提高。也许只用 protected 就够了（子类需要的不过如此）。也许同一程序集中的其他类确实需要访问。如果是这样，就提高到 internal。如果子类以及同一程序集中的其他类都需要访问，就使用 protected internal。只有那些应可供程序中每个类访问（无论程序集）的类（及其成员）才使用 public。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_417_1.png)

适用于整个类的建议同样适用于类成员：让它们尽可能不可访问。小型辅助类，或支持更公开类实现的类，可以限制为不超过 internal 的访问级别。

如果某个类或其他类型需要是 private、protected 或 protected internal，那么如果可以，请把它嵌套在需要访问它的类内部。

## 将类放入命名空间

命名空间的存在是为了把相关的类放进同一个容器，并减少不同位置所用名称之间的冲突。例如，你可以把所有与数学相关的类编译到一个 MathRoutines 命名空间中。
