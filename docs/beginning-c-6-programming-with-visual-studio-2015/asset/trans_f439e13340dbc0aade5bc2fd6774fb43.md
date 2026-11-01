
![](img/cf72ea860016d2d680fc085fc06f265a_306_0.png)

图 11-6

## 工作原理

本示例说明使用 is 运算符时可能出现的各种结果。定义了三个类、一个接口和一个结构体，并将它们用作某个类的一个方法的参数，该方法使用 is 运算符来确定它们是否可以转换为 ClassA 类型、接口类型和结构体类型。

只有 ClassA 和 ClassD（继承自 ClassA）类型与 ClassA 兼容。未继承自某个类的类型与该类不兼容。

ClassA、ClassB 和 MyStruct 类型都实现了 IMyInterface，因此它们都与 IMyInterface 类型兼容。ClassD 继承自 ClassA，因此它也兼容。因此，只有 ClassC 不兼容。

最后，只有 MyStruct 类型本身的变量以及该类型的装箱变量与 MyStruct 兼容，因为你不能将引用类型转换为值类型（当然，你可以解包先前已装箱的变量）。

## 值比较

考虑两个表示人的 Person 对象，每个对象都有一个整数类型的 Age 属性。你可能想比较它们以查看谁年纪更大。你可以简单地使用以下代码：

```
if (person1.Age > person2.Age)
{
    ...
}
```

```
=> (op1.val == op2.val);
public static bool operator !=(AddClass1 op1, AddClass1 op2)
=> !(op1 == op2);
public override bool Equals(object op1) => val == ((AddClass1)op1).val;
public override int GetHashCode() => val;
}
```

GetHashCode() 用于根据对象的状态为对象实例获取一个唯一的 int 值。这里使用 val 是可以的，因为它本身也是一个 int 值。

请注意 Equals() 使用 object 类型参数。你需要使用此签名，否则你将重载该方法而不是重写它，并且默认实现仍可供类的使用者访问。相反，你必须使用强制转换来获得所需的结果。在如下代码中，使用前面讨论过的 is 运算符检查对象类型通常是值得的：

```
public override bool Equals(object op1)
{
    if (op1 is AddClass1)
    {
        return val == ((AddClass1)op1).val;
    }
    else
    {
        throw new ArgumentException(
            "Cannot compare AddClass1 objects with objects of type "
            + op1.GetType().ToString());
    }
}
```

在此代码中，如果传递给 Equals 的操作数类型错误或无法转换为正确类型，则会抛出异常。当然，这种行为可能不是你想要的。你可能希望能够比较一种类型对象与另一种类型对象，在这种情况下需要更多的分支。或者，你可能希望将比较限制为两个对象类型完全相同的情况，这需要对第一个 if 语句进行如下更改：

```
if (op1.GetType() == typeof(AddClass1))
```

## 为 CardLib 添加运算符重载

现在你将再次升级你的 Ch11CardLib 项目，为 Card 类添加运算符重载。同样，你可以在本章代码下载的 Ch11CardLib 文件夹中找到以下类的代码。

不过首先，你将为 Card 类添加额外的字段，以允许使用王牌花色并提供将 A 牌置高的选项。你将它们设为 static，因为一旦设置，它们将适用于所有 Card 选项：

```
public class Card
{
    /// <summary>
    /// Flag for trump usage. If true, trumps are valued higher
    /// than cards of other suits.
    /// </summary>
```

```
public static bool useTrumps = false;
/// <summary>
/// Trump suit to use if useTrumps is true.
/// </summary>
public static Suit trump = Suit.Club;
/// <summary>
/// Flag that determines whether aces are higher than kings or lower
/// than deuces.
/// </summary>
public static bool isAceHigh = true;
```

这些规则适用于应用程序中每个 Deck 中的所有 Card 对象。不可能有两个牌堆，其中的牌遵循不同的规则。对于这个类库来说这是可以的，因为你可以安全地假设如果某个应用程序想要使用单独的规则，那么它可以自行维护这些规则，也许在切换牌堆时设置 Card 的静态成员。

由于你已经这样做了，值得为 Deck 类添加一些构造函数，以便用不同的特性初始化牌堆：

```
/// <summary>
/// Nondefault constructor. Allows aces to be set high.
/// </summary>
public Deck(bool isAceHigh) : this()
{
    Card.isAceHigh = isAceHigh;
}
/// <summary>
/// Nondefault constructor. Allows a trump suit to be used.
/// </summary>
public Deck(bool useTrumps, Suit trump) : this()
{
    Card.useTrumps = useTrumps;
    Card.trump = trump;
}
/// <summary>
/// Nondefault constructor. Allows aces to be set high and a trump suit
/// to be used.
/// </summary>
public Deck(bool isAceHigh, bool useTrumps, Suit trump) : this()
{
    Card.isAceHigh = isAceHigh;
    Card.useTrumps = useTrumps;
    Card.trump = trump;
}
```

这些构造函数都使用第 9 章中所示的 : this() 语法定义，因此在所有情况下，默认构造函数都会在非默认构造函数之前被调用，从而初始化牌堆。

> **注意** 在 == 和 > 运算符重载方法中实现的空条件运算符 (?.) 将在第 12 章中更详细地讨论。在 public static bool operator == 方法的此代码段中，card1?.suit 的 ?. 会在尝试检索 suit 中存储的值之前检查 card1 对象是否为 null。在后续章节实现该方法时这一点很重要。

现在将运算符重载（以及建议的重写）添加到 Card 类中：

```csharp
public static bool operator ==(Card card1, Card card2)
    => card1?.suit == card2?.suit && (card1?.rank == card2?.rank);
public static bool operator !=(Card card1, Card card2)
    => !(card1 == card2);
public bool Equals(object card) => this == (Card)card;
public override int GetHashCode()
    => return 13 * (int)suit + (int)rank;
public static bool operator >(Card card1, Card card2)
{
    if (card1.suit == card2.suit)
    {
        if (isAceHigh)
        {
            if (card1.rank == Rank.Ace)
            {
                if (card2.rank == Rank.Ace)
                    return false;
                else
                    return true;
            }
            else
            {
                if (card2.rank == Rank.Ace)
                    return false;
                else
                    return (card1.rank > card2?.rank);
            }
        }
        else
        {
            return (card1.rank > card2.rank);
        }
    }
    else
    {
        if (useTrumps && (card2.suit == Card.trump))
            return false;
        else
            return true;
    }
}
```

```
public static bool operator <(Card card1, Card card2)
    => !(card1 > card2);
public static bool operator >=(Card card1, Card card2)
{
    if (card1.suit == card2.suit)
    {
        if (isAceHigh)
        {
            if (card1.rank == Rank.Ace)
            {
                return true;
            }
            else
            {
                if (card2.rank == Rank.Ace)
                    return false;
                else
                    return (card1.rank >= card2.rank);
            }
        }
        else
        {
            return (card1.rank >= card2.rank);
        }
    }
    else
    {
        if (useTrumps && (card2.suit == Card.trump))
            return false;
        else
            return true;
    }
}
public static bool operator <=(Card card1, Card card2)
    => !(card1 > card2);
```

这里没什么特别需要注意的，除了 > 和 >= 重载运算符的代码稍长一些。如果你逐步执行 > 的代码，你可以看到它的工作原理以及为什么需要这些步骤。

你正在比较两张牌 card1 和 card2，其中假设 card1 是先放在桌上的那张。如前所述，当使用王牌时这一点变得很重要，因为王牌会击败非王牌，即使非王牌的点数更高。当然，如果两张牌的花色相同，那么花色是否为王牌花色就无关紧要了，所以这是你做的第一个比较：

```
public static bool operator >(Card card1, Card card2)
{
    if (card1.suit == card2.suit)
    {
```
