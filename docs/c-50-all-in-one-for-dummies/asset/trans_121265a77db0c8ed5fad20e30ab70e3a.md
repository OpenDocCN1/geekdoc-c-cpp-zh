
其他。假设 GroupA 是秘密 X 的持有者，因此该组将其标记为私有。代码看起来如下：

```assembly
// 在程序 InternalLimitsAccess 中：
class Congress
{
    static void Main(...)
    {
        // 监督 CIA 的代码
    }
}

// 在程序 CIAAssembly 中：
public class GroupA
{
    private string _secretFormulaForCocaCola; // Secret X
    internal GroupA() { _secretFormulaForCocaCola = "lots of sugar";
}
public class GroupB
{
    public void DoSomethingWithSecretX()
    {
        // 对秘密 X 做些什么，只要你能访问它的话。
    }
}
```

现在 GroupB 无法看到秘密 X，但假设它有合法的需要需要知道它。GroupA 然可以将秘密 X 提升为公开状态，但如果它这样做，这个秘密就不再是一个真正的秘密了。如果 GroupB 能看到这个秘密，国会里的那些窥探者也能看到。糟糕的是，CNN 也知道，更不用说 Fox、ABC 和其他频道了。你你知道那些人守秘密守有多好。噢，对了——俄罗斯也能看到秘密 X。

![](img/6df7bb88e9302e98442acc219cfbd7fc_409_0.png)

幸运的是，C# 还有 `internal` 关键字。使用 `internal` 仅比 `public` 低一级，但远高于 `private`。如果你用 `internal` 关键字标记 GroupA 类及其“公开”方法（即那些在类外部可见的方法），那么 CIA 的每个人都可以看到并访问秘密 X ——只要你将秘密本身（一个数据成员）也标记为内部，或者提供一个内部属性来获取它，如下版本所示：

```assembly
// 在程序 CIAAssembly 中：
internal class GroupA
{
    private string _secretFormulaForCocaCola; // Secret X
    internal string SecretX { get { return _secretFormulaForCocaCola; } }
    internal GroupA() { _secretFormulaForCocaCola = "lots of sugar";
}
public class GroupB
{
    public void DoSomethingWithSecretX()
    {
        // 既然我们能看到它了，对秘密 X 做些什么：
        Console.WriteLine("I know Secret X, which is {0} characters long, but " + "I'm not telling.", GroupA.SecretX.Length);
    }
}
```

## 超越公开与私有：更多访问关键字 385

现在 GroupB 类拥有了它需要的访问权限 —— 它并没有交出秘密（即使在水刑的威胁下）。它在 Main() 中告诉国会的只有它知道秘密 X，而且秘密 X 有 11 个字符。这里是那段代码：

```csharp
class Congress
{
    static void Main(string[] args)
    {
        // 监督 CIA 的代码
        // 下行无法编译，因为 GroupA 在 CIAAssembly 外部是不可访问的
        // 国会无法突破 CIA。

        // CIAAssembly.GroupA = new CIAAssembly.GroupA();
        // 类无法访问 GroupB，因为它是公开的。
        // GroupB 愿意知道这个秘密，但它
        // 不告诉——除非给出一个小提示。
        GroupB groupB = new GroupB();
        groupB.SomethingWithSecretX();
    }
    Console.WriteLine("Press Enter to terminate...");
    Console.Read();
}
```

从 Main() 来看，GroupA 是不可见的，因此无法尝试构造它的实例。但因为 GroupB 是公开的，Main() 可以访问并调用它的公开方法 DoSomethingWithSecretX()。

等一下！CIA 必须与国会讨论某些话题，我很高兴地报告 —— 但基于“需情知晓”原则，仅限于选定的国会成员和参议员，你可以通过 GroupB 这样做，只要他们出示正确的凭据，尽管你仍然将它们添加到代码中：

```csharp
public string SomethingWithSecretXUsingCredentials(string credentials)
{
    if (credentials == "congressman with approved access")
    {
        return GroupA.SecretX;
    }
    return String.Empty;
}
```

`internal` 关键字使得类和成员仅在它们自己的程序集（assembly）内部可访问。但在程序集内部，`internal` 项目实际上对所有本地类都是“公开”的。

你可以将 `internal` 类内部的方法标记为 `public`，尽管它并非真正的公开。类成员的访问权限不能高于其所属类，所以所谓的“公开”成员其实只是 `internal`。

![](img/6df7bb88e9302e98442acc219cfbd7fc_410_0.png)

CIA 仍然可以通过在所属类内部将秘密声明为 `private`，从而保持其最深、最黑暗的秘密绝对机。这种策略使得它们仅在该类中可访问。

## Protected：与子类共享

`private` 的主要目的是隐藏信息。特别是，`private` 隐藏了类的内部实现细节。（与类之间关系过于亲密的类并不是世界上最幸运的类。事实上，它们是最倒霉的类。）具有大量实现细节的类被认为与它们了解过多的类“过度耦合”。如果类 A 知道类 B 的内部工作机制，A 可能会过度依赖这些细节。如果这些细节发生变化，你最终不得不修改两个类。

其他类 —— 以及程序集 —— 对类 B 如何执行其魔法了解得越少越好。在本部微型书籍的第 5 章中，我使用了 `BankAccount` 类作为示例。银行不希望像我这样健忘的人 —— 或者像类 A 这样健忘的类 —— 直接修改余额。该余额恰恰属于 `BankAccount` 类的实现。它是 `private` 的。`BankAccount` 提供对余额的访问 —— 但仅通过经过仔细控制的公开接口。在 `BankAccount` 类中，公开接口由三个公开方法组成：

- ♦ Balance：提供了一种只读的方法来查找当前余额。你不能使用 `Balance` 来修改底层余额。
- ♦ Deposit()：允许类外部的人受控地增加余额。
- ♦ Withdraw()：允许某人（可能是账户所有者）从余额中扣款，但受到仔细控制的限制。`Withdraw()` 强制执行了你不能提取超过持有金额的业务规则。

编程中除了 `private` 和 `public` 之外，还有其他访问控制的考虑。我在上一节中解释了 `internal` 关键字如何开放一个类 —— 但仅对其所在程序集中的其他类开放。

然而，假设 `BankAccount` 类有一个子类 `SavingsAccount`。`SavingsAccount` 中的方法需要访问基类中定义的该余额。幸运的是，你可以通过 `GroupB` 这样做，只要他们出示正确的凭据，尽管你仍然将它们添加到代码中（此处原文重复上文逻辑，已修正翻译逻辑对应）：假设 `BankAccount` 类有一个子类 `SavingsAccount`。`SavingsAccount` 中的方法需要访问基类中定义的该余额。幸运的是，你可以通过公开接口访问它，例如使用 `Balance`、`Deposit()` 和 `Withdraw()`。

但有时，基类并没有为子类提供此类访问方法。如果 `BankAccount` 中的 `_balance` 是 `private` 的，且类没有提供 `Balance` 属性怎么办？

![](img/6df7bb88e9302e98442acc219cfbd7fc_412_0.png)

输入 `protected` 关键字：如果基类中的实例变量被声明为 `protected` 而不是 `private`，那么它对外部人员实际上是私有的。但子类可以正常看到。

另一种更好的解决方案是在 `BankAccount` 中将 `_balance` 标记为 `private`，然后提供一个标记为 `protected` 的 `Balance` 属性。子类如 `SavingsAccount` 就可以通过 `Balance` 属性访问 `_balance`。

如果余额确实需要对外部人员公开（只读），你理应提供公开的 `Balance` 属性来获取余额。然而，你可能还需要 `SavingsAccount` 内部设置余额。为了这一点，你可以将 `Balance` 的设置访问器设置为 `protected` —— 对 `SavingsAccount` 可用但对外部人员不可用。

```csharp
// 在 BankAccount 中
public decimal Balance
{
    get { return _balance; }      // 公开
    protected set { _balance = value; }  // 非公开
}
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_412_1.png)

网上的 `ProtectedAccess` 示例说明了上述如何使用 `protected`。

你甚至可以在另一个程序集中派生 `BankAccount`，并且子类可以访问 `BankAccount` 中声明为 `protected` 的任何内容。`ProtectedAccess` 示例也说明了这个过程。

该示例有两个 `BankAccount` 的子类：一个与 `BankAccount` 在同一个程序集中，另一个在不同的程序集中。关于 `protected` 有趣的是，任何 `BankAccount` 子类都可以访问 `BankAccount` 中标记为 `protected` 的项。子类不需要与其基类位于同一个程序集中。

从程序集外部扩展（派生）类的能力涉及到安全问题，这就是为什么许多类应该是 `sealed` 的。密封类可以防止外部通过子类化来获取访问。这就是为什么我们建议只有在类需要被子类化时才将其设置为可扩展的（非密封的）。让同一程序集内的其他代码访问基类成员（包括同一程序集中的子类）的一种方法是将这些成员标记为 `internal` 而不是 `protected`。

