
```csharp
class AccountTest
{
    public static void Main ()
    {
        Account test = new Account();
        test.PayInterest (50);
        Console.WriteLine ("Balance:" + test.GetBalance());
    }
}
```

AccountTest 类有一个名为 Main 的静态成员方法。我们知道这是运行程序时被调用的方法。它是 AccountTest 类的一部分。如果我创建了五十个 AccountTest 实例，它们都会共享同一个 Main 方法。在 C# 术语中，关键字 static 用于标记成员属于类本身，而不属于类的实例。我将再次用漂亮的字体写下来，

> > “静态成员是类的成员，而不是类的实例的成员”

我不需要创建 AccountTest 类的实例就能使用 Main 方法。这就是我的程序实际运行的方式，因为当它启动时还没有创建任何实例，因此该方法必须已经存在，否则它无法运行。

Static 并不是指“不可更改”。我想这时候该用更多漂亮的字体了：

> > Static 并不是指“不可更改”。

被设为静态的类成员可以像类的任何其他成员一样使用。数据成员或方法都可以设为静态。

## 4.6.2 使用类的静态数据成员

也许在这个时候举一个静态数据的例子会有帮助。考虑我们的银行账户的利率。客户告诉我们，账户类的一个成员需要是账户的利率。在程序中，我们可以通过向类添加另一个成员来实现这一点，该成员保存当前的利率：

```csharp
public class Account
{
    public decimal Balance ;
    public decimal InterestRateCharged ;
}
```

现在我可以创建账户并为它们设置余额和利率。（当然，如果我做得规范，我会将这些设为私有并提供方法等，但我现在保持简单。）

```csharp
Account RobsAccount = new Account();
RobsAccount.Balance = 100;
RobsAccount.InterestRateCharged = 10;
```

问题在于我被告知利率适用于所有账户。如果利率发生变化，它必须对所有账户都生效。这意味着要实现更改，我必须遍历所有账户并更新利率。这会很繁琐，而且如果漏掉一个账户，可能会很昂贵。

我通过将利率成员设为静态来解决这个问题：

```csharp
public class Account
{
    public decimal Balance ;
    public static decimal InterestRateCharged ;
}
```

利率现在是类的一部分，而不是任何实例的一部分。这意味着我必须改变获取它的方式：

```csharp
Account RobsAccount = new Account();
RobsAccount.Balance = 100;
Account.InterestRateCharged = 10;
```

由于它是类的成员，现在我必须使用类名来获取它，而不是实例引用的名称。

### 程序员提示：静态数据成员很有用但也很危险

当你为项目收集元数据时，应该寻找可以设为静态的东西。像值的限制（你将允许一个人拥有的最大年龄）之类的东西可以设为静态。可能有一天年龄限制会发生变化，而你不想更新程序中的所有对象。

但当然，正如蜘蛛侠的叔叔所说，“能力越大，责任越大。”你应该小心如何提供对静态数据项的访问。对单个静态值的更改会影响整个系统。因此它们应始终设为私有，并通过方法调用进行更新。

## 4.6.3 在类中使用静态方法

我们也可以使方法静态。我们很久以来一直对 Main 方法这样做。但在设计系统时你也可以使用它们。例如，我们可能有一个方法来决定某人是否被允许拥有银行账户。它会接收年龄和收入。然后根据这些是否可接受返回 true 或 false：

```csharp
public bool AccountAllowed ( decimal income, int age )
{
    if ( ( income >= 10000 ) && ( age >= 18 ) )
    {
        return true;
    }
    else {
        return false;
    }
}
```

这会检查年龄和收入；你必须年满 17 岁并且至少有 10000 英镑的收入才被允许开户。问题是，目前我们必须先拥有一个 Account 实例才能调用该方法。我们可以通过使方法静态来解决这个问题：

```csharp
public static bool AccountAllowed ( decimal income, int age )
{
    if ( ( income >= 10000 ) && ( age >= 18 ) )
    {
        return true;
    }
    else {
        return false;
    }
}
```

现在该方法属于类，而不是类的实例。我现在可以通过使用类名来调用该方法：

```csharp
if ( Account.AccountAllowed ( 25000, 21 ) )
{
    Console.WriteLine ( "Allowed Account" );
}
```

这很好，因为我不需要创建账户实例就能查明是否允许开户。

### 在静态方法中使用成员数据

Allowed 方法没问题，但当然我已将年龄和收入固定在其中。我可能会决定使方法更灵活：

```csharp
public class Account
{
    private decimal minIncome = 10000;
    private int minAge = 18;

    public static bool AccountAllowed(decimal income, int age)
    {
        if ( ( income >= minIncome ) && ( age >= minAge ) )
        {
            return true;
        }
        else
        {
            return false;
        }
    }
}
```

这是一个更好的设计，因为我现在拥有类成员来设定年龄和收入的上限。然而这是一个糟糕的程序，因为上面的类无法编译：

```
AccountManagement.cs(19,21): error CS0120: An object reference is required for the nonstatic field, method, or property 'Account.minIncome'
AccountManagement.cs(19,43): error CS0120: An object reference is required for the nonstatic field, method, or property 'Account.minAge'
```

像往常一样，编译器正用让人头晕的语言告诉我们到底哪里错了。编译器真正的意思是“静态方法正在使用一个非静态的类成员。”

如果这没有帮助，试试这个。成员 minIncome 和 minAge 保存在 Account 类的实例中。然而，静态方法可以在没有实例的情况下运行（因为它属于类）。编译器不满意，因为在这种情况下方法将没有任何成员可供使用。我们可以通过也将收入和年龄限制设为静态来修复这个问题（并使程序完全正确）：

```csharp
public class Account
{
    private static decimal minIncome ;
    private static int minAge ;

    public static bool AccountAllowed(decimal income, int age)
    {
        if ( ( income >= minIncome ) && ( age >= minAge ) )
        {
            return true;
        }
        else
        {
            return false;
        }
    }
}
```

如果你想想，这完全说得通。限制值不应该作为类的成员保存，因为我们希望它们对所有实例都相同，因此，将它们设为静态是我们一开始就应该做的。

### 程序员提示：静态方法成员可用于创建库

有时在开发中你需要提供一组执行任务的方法。在 C# 系统本身中，有大量用于执行数学函数的方法，例如 sin 和 cos。在这种情况下我们只需要方法本身，而不是类的实例，因此将这些方法设为静态是有意义的。同样，在构建系统时，你应该考虑如何使此类方法为你自己的使用提供可用。

## 银行笔记：静态银行信息

我们可以在银行中使用 static 解决的问题类型有：

**static member variable:** 管理员希望我们能够一次性为所有客户账户设置利率。Account 类的单个静态成员将提供一个可在所有实例内部使用的变量。但由于该值只有一个副本，因此可以更改它，从而调整所有账户的利率。任何对所有类只保存一次的值（值的限制是另一个例子）最好作为静态值管理。当管理员说“哦，五岁儿童的账户利率与普通账户不同”时，使用静态就变得不可能了。此时我们知道不能使用静态，因为我们需要为某些实例保存不同的值。

**static member method:** 管理员告诉我们需要一个方法来确定某人是否被允许拥有账户。我不能将其作为任何 Account 实例的一部分，因为在运行时账户尚未生成。我必须将其设为静态，以便它可以在没有实例的情况下执行。

## 4.7 对象的构造

我们已经看到，当我们使用 new 来创建对象时，我们的对象就被创建了：

```csharp
test = new Account();
```

如果你仔细观察正在发生的事情，你可能会认为这看起来很像一次方法调用。

这实际上正是正在发生的事情。当创建类的实例时，C# 系统会调用该类中的构造函数方法。构造函数方法是类的成员，它的作用是让程序员获得控制权并设置这个崭新对象的内部内容。C# 游戏规则之一是每个类都必须有一个构造函数方法，以便在创建新实例时调用。
