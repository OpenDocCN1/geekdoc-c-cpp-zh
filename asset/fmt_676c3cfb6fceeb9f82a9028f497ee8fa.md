
该类有两个 `readonly` 字段，分别代表牌的数值和花色。构造函数初始化了这些字段。

> `readonly` 字段用于建模在初始化后不应更改的数据。你可以在声明字段时使用初始化器或在构造函数中为 `readonly` 字段赋值，但此后你就无法对其进行修改了。

该类包含一对方法 `CardValue` 和 `CardSuit`，它们用于返回这些信息，并重写了 `ToString` 方法以返回牌的字符串表示。

> `CardValue` 和 `CardSuit` 方法实际上实现为属性（properties）更好，你将在第 15 章中学习它们。

### 10. 在代码和文本编辑器窗口中打开 `Pack.cs` 文件。
该文件包含 `Pack` 类，模拟了一副扑牌。在 `Pack` 类的顶部有两个名为 `NumSuits` 和 `CardsPerSuit` 的 `public const int` 字段。这两个字段指定了牌牌中花色的数量以及每种花色的牌数。
`private cardPack` 变量是一个 `PlayingCard` 对象的二维数组。你将使用第一个维度来指定花色，使用第二个维度来指定花色中牌的数值。
`randomCardSelector` 变量是基于 `Random` 类生成的随机数。你将使用 `randomCardSelector` 变量在发发给每个手之前帮助进行洗牌。

[点击此处查看代码图片]

### 11. 找到 `Pack` 类的默认构造函数。目前，该构造函数除了一个 `// TODO:` 注释外是空的。删除该注释并添加此处**加粗**的语句，以使用每个维度的适当值实例化 `cardPack` 数组：

[点击此处查看代码图片]

```csharp
public Pack()
{
    this.cardPack = new PlayingCard[NumSuits, CardsPerSuit];
}
```

### 12. 在 `Pack` 构造函数中添加以下**加粗**的代码。这些语句将 `cardPack` 数组填充为完整且排序后的牌组。

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

### 13. 找到 `Pack` 类中的 `DealCardFromPack` 方法。该方法的目的是从牌中随机抽取一张牌，将其从牌中移除以防止再次被选中，然后将其作为方法的返回值传回。

该方法的第一个任务是随机选择一个花色。删除该方法中抛出异常的语句并将其替换为以下内容：

```csharp
public PlayingCard DealCardFromPack()
{
    var suit = (Suit)randomCardSelector.Next(NumSuits);
}
```

该语句使用随机生成器的 `Next` 方法来选择花色。请注意返回的值在 0 和上限值之间。你需要处理没有剩余该花色牌牌的情况。

### 14. 在选择花色的代码之后，添加以下循环以判断该花色是否还有剩余牌。如果没有，则再次选择另一个花色：

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

### 15. 在 `DealCardFromPack` 方法的现有代码之后，添加以下**加粗**的语句以随机选择一个牌的值：

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

### 16. 现在你选择了一张尚未发过的随机牌。在 `DealCardFromPack` 方法中添加以下代码返回此牌，并将 `cardPack` 数组中相应的元素置为 `null`：

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

### 17. 找到 `IsNotEmpty` 方法。记住该方法的目的是接收一个 `Suit` 参数并返回一个布尔值，表示牌中是否还存在该花色的牌。删除该方法中的注释和抛出 `NotImplementedException` 的语句，然后添加以下**加粗**的代码：

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

### 18. 找到 `IsCardDealt` 方法。该方法的目的是确定指定花色和数值的牌是否已经发牌并从牌中移除。稍后你会看到，当 `DealCardFromPack` 方法发牌时，它会将牌从 `cardPack` 数组中移除并将相应的元素置为 `null`。用此处**加粗**的代码替换该方法的主体：

[点击此处查看代码图片]

```csharp
private bool IsCardAlreadyDealt(Suit suit, Value value)
=> (this.cardPack[(int)suit, (int)value] == null);
```

如果 `cardPack` 数组中对应于花色和值的元素为 `null`，则该方法返回 `true`，否则返回 `false`。

### 19. 下一步是将选定的扑牌添加到手中。打开 `Hand.cs` 文件并在“代码和文本编辑器”窗口显示它。该文件包含 `Hand` 类，该类实现了一个手牌（即发给玩家的所有牌）。

该文件包含一个名为 `HandSize` 的 `public const int`，其值被设置为手牌的大小（13）。它还包含一个 `PlayingCard` 对象的数组，该数组使用 `HandSize` 常量初始化。你的代码将使用 `playingCount` 字段在填充手牌时跟踪手中目前有多少张扑牌。

点击此处查看代码图片

```csharp
class Hand
{
    public const int HandSize = 13;
    private PlayingCard[] cards = new PlayingCard[HandSize];
    private int playingCardCount = 0;
}
```

`ToString` 方法生成手牌扑牌的字符串表示。它使用 `foreach` 循环遍历 `cards` 数组中的项，并对找到的每个 `PlayingCard` 对象调用 `ToString` 方法。为了格式化，这些字符串之间用换行符连接（使用 `Environment.NewLine` 常量来指定换行符）。

点击此处查看代码图片

```csharp
public override string ToString()
{
    string result = "";
    foreach (PlayingCard card in this.cards)
    {
        result += $"{card.ToString()}{Environment.NewLine}";
    }
    return result;
}
```

### 20. 在 `Hand` 类中找到 `AddCardToHand` 方法。该方法的作用是将参数中指定的扑牌添加到手中。删除注释并向该方法添加以下**粗体**所示的语句：

点击此处查看代码图片

```csharp
public void AddCardToHand(PlayingCard cardDealt) {
    if (this.playingCardCount >= HandSize) {
        throw new ArgumentException("Too many cards");
    }
    this.cards[this.playingCardCount] = cardDealt;
    this.playingCardCount++;
}
```

这段代码检查手中是否已经满额。如果手中已满，它将抛出一个 `ArgumentException`（这永远不应该发生，但为了安全是良好的做法）。否则，扑牌会被添加到 `playingCardCount` 变量指定的索引 `cards` 数组中，并且该变量加增。

### 21. 在“解决方案管理器”中，展开 `MainPage.xml` 节点，然后在“代码和文本编辑器”窗口中打开 `MainPage.xml.cs` 文件。这是游戏窗口的代码。

### 22. 找到 `dealClick` 方法。该方法在用户选择“发牌（Deal）”按钮时运行。目前，它包含一个空的 `try` 块和一个在发生异常时显示消息的异常处理程序。

### 23. 删除注释并向 `try` 块添加以下**粗体**所示的语句：

点击此处查看代码图片

```csharp
private void dealClick(object sender, RoutedEventArgs e) {
    try {
        pack = new Pack();
    }
    catch (Exception ex) {
        ...
    }
}
```

此语句仅用于创建一个新的牌包。你之前看到过该类包含一个持有扑牌的二维数组，构造函数向该数组中填充了每张牌的详情。你现在需要从这个牌包中创建四手牌。

### 24. 向 `try` 块添加以下**粗体**所示的语句：

点击此处查看代码图片

```csharp
try {
    pack = new Pack();
    for (var handNum = 0; handNum < NumHands; handNum++) {
        hands[handNum] = new Hand();
    }
}
catch (Exception ex) {}
```

此循环从牌包创建四手牌并将它们存储在 `hands` 数组中。每个手最初是空的，因此你需要将牌包中的牌发到每个手中。

### 25. 在 `for` 循环中添加以下**粗体**所示的代码：

点击此处查看代码图片

```csharp
try {
    pack = new Pack();
    for (var handNum = 0; handNum < NumHands; handNum++) {
        hands[handNum] = new Hand();
        for (var numCards = 0; numCards < Hand.HandSize; numCards++) {
            var cardDealt = pack.DealCardFromPack();
            hands[handNum].AddCardToHand(cardDealt);
        }
    }
}
catch (Exception ex) {
    ...
```

内部 `for` 循环使用 `DealCardFromPack` 方法从牌包随机获取牌，并使用 `AddCardToHand` 方法将此牌添加到手中。

### 26. 在外部 `for` 循环之后添加以下**粗体**所示的代码：

点击此处查看代码图片

牌包中的牌应随机发到每个手中，每个手中的牌应如如下图像所示：

![](img/4fc1423eceeb79a4e5db8b1746d20.png)

### 28. 再次选择 Deal。验证发了一组新牌，并且每个手中的牌发生了变化。

### 29. 返回 Visual Studio 并停止调试。

## 访问值类型数组

你可以将数组视为按索引排序的简单数据集合。如果你知道索引，可以轻松获取项；但如果你想根据其他属性查找数据，通常需要实现一个执行并返回所需项索引的方法。

例如，考虑以下创建 `Person` 对象数组的代码，其中 `Person` 是一个类：

点击此处查看代码图片

```csharp
class Person
{
    public string Name;
    public int Age;
    public Person(string name, int age)
    {
        this.Name = name;
        this.Age = age;
    }
}
```

```csharp
var names = new[] { 
    new { Name = "John", Age = 57 },
    new { Name = "Diana", Age = 57 },
    new { Name = "James", Age = 30 },
    new { Name = "Francesca", Age = 26 } 
};
```

你想找到 `Person` 数组中年龄最小的成员，因此你编写了以下方法：

```csharp
Person findYoungest()
{
    int youngest = 0;
    for (int i = 1; i < family.Length; i++)
    {
        if (family[i].Age < family[youngest].Age)
        {
            youngest = i;
        }
    }
    return family[youngest];
}
```

你可以按照以下方式调用它并显示结果：

点击此处查看代码图片

```csharp
var mostYouthful = findYoungest();
Console.WriteLine($"Name: {mostYouthful.Name}, Age: {mostYouthful.Age}");
```

希望显示如下结果：

Francesca, Age: 26

这非常满意且运行良好。接下来，你想更新最小成员的年龄（Francesca 刚过生日，现在是 27），所以你写了以下语句：

```csharp
mostYouthful.Age++;
```

最后，为了确认所有内容已正确更改，你使用以下语句遍历 `family` 数组并显示其内容：

点击此处查看代码图片

```csharp
foreach (Person familyMember in family)
{
    Console.WriteLine($"Name: {familyMember.Name}, Age:{familyMember.Age}");
}
```

你高兴地观察到结果是正确的，Francesca 的年龄已被修改：

```
John, Age: 57
Diana, Age: 57
James, Age: 30
Francesca, Age: 27
```
