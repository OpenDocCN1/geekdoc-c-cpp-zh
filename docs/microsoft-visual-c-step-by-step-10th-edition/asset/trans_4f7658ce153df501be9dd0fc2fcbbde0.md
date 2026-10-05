

```csharp
enum Value ( Two, Three, Four, Five, Six, Seven, Eight, Nine, Ten, Jack, Queen, King, Ace )
```

8. 在代码和文本编辑器中打开 `Suit.cs` 文件。

该文件包含一个名为 `Suit` 的枚举，代表了标准牌中的花色：

[点击此处查看代码图片]

```csharp
enum Suit { Clubs, Diamonds, Hearts, Spades }
```

9. 在代码和文本编辑器中打开 `PlayingCard.cs` 文件。

该文件包含 `PlayingCard` 类。该类模拟了单张扑牌。

[点击此处查看代码图片]

```csharp
class PlayingCard
{
    private readonly Suit suit;
    private readonly Value value;

    public PlayingCard(Suit s, Value v)
    {
        this.suit = s;
        this.value = v;
    }

    public override string toString()
    {
        string result = $"{this.value} of {this.suit}";
        return result;
    }

    public Suit CardSuit()
    {
        return this.suit;
    }

    public Value CardValue()
    {
        return this.value;
    }
}
```

该类有两个 `readonly` 字段，分别代表牌的数值和花色。构造函数初始化了这些字段。

> `readonly` 字段用于建模在初始化后不应更改的数据。你可以在声明字段时使用初始化器或在构造函数中为 `readonly` 字段赋值，但此后你就无法对其进行修改了。

该类包含一对方法 `CardValue` 和 `CardSuit`，它们用于返回这些信息，并重写了 `ToString` 方法以返回牌的字符串表示。

> `CardValue` 和 `CardSuit` 方法实际上实现为属性（properties）更好，你将在第 15 章中学习它们。

- 10. 在代码和文本编辑器窗口中打开 `Pack.cs` 文件。
该文件包含 `Pack` 类，模拟了一副扑牌。在 `Pack` 类的顶部有两个名为 `NumSuits` 和 `CardsPerSuit` 的 `public const int` 字段。这两个字段指定了牌牌中花色的数量以及每种花色的牌数。
`private cardPack` 变量是一个 `PlayingCard` 对象的二维数组。你将使用第一个维度来指定花色，使用第二个维度来指定花色中牌的数值。
`randomCardSelector` 变量是基于 `Random` 类生成的随机数。你将使用 `randomCardSelector` 变量在发发给每个手之前帮助进行洗牌。

[点击此处查看代码图片]

- 11. 找到 `Pack` 类的默认构造函数。目前，该构造函数除了一个 `// TODO:` 注释外是空的。删除该注释并添加此处**加粗**的语句，以使用每个维度的适当值实例化 `cardPack` 数组：

[点击此处查看代码图片]

```csharp
public Pack()
{
    this.cardPack = new PlayingCard[NumSuits, CardsPerSuit];
}
```

- 12. 在 `Pack` 构造函数中添加以下**加粗**的代码。这些语句将 `cardPack` 数组填充为完整且排序后的牌组。

[点击此处查看代码图片]

```csharp
public Pack()
{
    this.cardPack = new PlayingCard[NumSuits, CardsPerSuit];
    for (var suit = Suit.Clubs; suit <= Suit.Spades; suit++)
    {
        for (var value = Value.Two; value <= Value.Ace; value++)
        {
            this.cardPack[(int)suit, (int)value] = new PlayingCard(suit, value);
        }
    }
}
```

外部 `for` 循环遍历 `Suit` 枚举中的值列表，而内部 `for` 循环遍历每种花色中牌可以拥有的值。内部 `for` 循环还会创建一个指定花色和数值的新 `PlayingCard` 对象，并将其添加到 `cardPack` 数组相应的元素中。

> 你必须使用整数类型之一作为数组的索引。`suit` 和 `value` 变量是枚举变量。然而，枚举是基于整数类型的，因此如代码所示将它们强制转换为 `int` 是安全的。

- 13. 找到 `Pack` 类中的 `DealCardFromPack` 方法。该方法的目的是从牌中随机抽取一张牌，将其从牌中移除以防止再次被选中，然后将其作为方法的返回值传回。

该方法的第一个任务是随机选择一个花色。删除该方法中抛出异常的语句并将其替换为以下内容：

```csharp
public PlayingCard DealCardFromPack()
{
    var suit = (Suit)randomCardSelector.Next(NumSuits);
}
```

该语句使用随机生成器的 `Next` 方法来选择花色。请注意返回的值在 0 和上限值之间。你需要处理没有剩余该花色牌牌的情况。

- 14. 在选择花色的代码之后，添加以下循环以判断该花色是否还有剩余牌。如果没有，则再次选择另一个花色：

[点击此处查看代码图片]

```csharp
public PlayingCard DealCardFromPack()
{
    var suit = (Suit)randomCardSelector.Next(NumSuits);
    while (!IsNotEmpty(suit))
    {
        suit = (Suit)randomCardSelector.Next(NumSuits);
    }
}
```

该循环调用 `IsNotEmpty` 方法来判断该花色是否有剩余牌。如果是，则重复该过程直到找到有剩余牌的花色为止。

- 15. 在 `DealCardFromPack` 方法的现有代码之后，添加以下**加粗**的语句以随机选择一个牌的值：

[点击此处查看代码图片]

```csharp
public PlayingCard DealCardFromPack()
{
    var suit = (Suit)randomCardSelector.Next(NumSuits);
    while (!IsNotEmpty(suit))
    {
        suit = (Suit)randomCardSelector.Next(NumSuits);
    }
    var value = (Value)randomCardSelector.Next(CardsPerSuit);
    while (IsCardDealt(suit, value))
    {
        value = (Value)randomCardSelector.Next(CardsPerSuit);
    }
}
```

- 16. 现在你选择了一张尚未发过的随机牌。在 `DealCardFromPack` 方法中添加以下代码返回此牌，并将 `cardPack` 数组中相应的元素置为 `null`：

[点击此处查看代码图片]

```csharp
public PlayingCard DealCardFromPack()
{
...
    var card = this.cardPack[(int)suit, (int)value];
    this.cardPack[(int)suit, (int)value] = null;
    return card;
}
```

- 17. 找到 `IsNotEmpty` 方法。记住该方法的目的是接收一个 `Suit` 参数并返回一个布尔值，表示牌中是否还存在该花色的牌。删除该方法中的注释和抛出 `NotImplementedException` 的语句，然后添加以下**加粗**的代码：

[点击此处查看图片]

```csharp
private bool IsNotEmpty(Suit suit)
{
    bool result = true;
    for (var value = Value.Two; value <= Value.Ace; value++)
    {
        if (!IsCardDealt(suit, value))
        {
            result = false;
            break;
        }
    }
    return result;
}
```

- 18. 找到 `IsCardDealt` 方法。该方法的目的是确定指定花色和数值的牌是否已经发牌并从牌中移除。稍后你会看到，当 `DealCardFromPack` 方法发牌时，它会将牌从 `cardPack` 数组中移除并将相应的元素置为 `null`。用此处**加粗**的代码替换该方法的主体：

[点击此处查看代码图片]

