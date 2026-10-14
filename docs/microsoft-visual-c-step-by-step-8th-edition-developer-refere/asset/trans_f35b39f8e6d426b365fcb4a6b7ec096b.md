

```
this.cardPack = new Dictionary<Suit, List<PlayingCard>>
(NumSuits);
...
}
```

尽管 Dictionary 集合会在添加项时自动调整大小，但如果集合的大小不太可能发生变化，你可以在实例化时指定初始大小。这有助于优化内存分配（尽管 Dictionary 集合在超过此大小时仍可以增长）。在这种情况下，Dictionary 集合将包含四个列表的集合（每种花色一个列表），因此为四个项分配了空间（NumSuits 是一个值为 4 的常量）。

6. 在外部 for 循环中，声明一个名为 cardsInSuit 的 List<PlayingCard> 集合对象，其大小足以容纳每种花色的牌数（使用 CardsPerSuit 常量），如下所示加粗部分：

Click here to view code image

```
public Pack()
{
    this.cardPack = new Dictionary<Suit, List<PlayingCard>>
(NumSuits);

    for (Suit = Suit.Clubs; suit <= Suit.Spades; suit++)
    {
        List<PlayingCard> cardsInSuit = new List<PlayingCard>
(CardsPerSuit);
        for (Value value = Value.Two; value <= Value.Ace;
value++)
        {
            ...
        }
    }
}
```

7. 修改内部 for 循环中的代码，将新的 PlayingCard 对象添加到此集合而不是数组中，如以下代码中加粗所示：

Click here to view code image

```
for (Suit suit = Suit.Clubs; suit <= Suit.Spades; suit++)
{
    List<PlayingCard> cardsInSuit = new List<PlayingCard>
(CardsPerSuit);
    for (Value value = Value.Two; value <= Value.Ace; value++)
    {
        cardsInSuit.Add(new PlayingCard(suit, value));
    }
}
```

8. 在内部 for 循环之后，将 List 对象添加到 cardPack Dictionary 集合中，并指定 suit 变量的值作为此项的键：

Click here to view code image

```
for (Suit suit = Suit.Clubs; suit <= Suit.Spades; suit++)
{
    List<PlayingCard> cardsInSuit = new List<PlayingCard>
(CardsPerSuit);
    for (Value value = Value.Two; value <= Value.Ace; value++)
    {
        cardsInSuit.Add(new PlayingCard(suit, value));
    }
    this.cardPack.Add(suit, cardsInSuit);
}
```

## 9. 找到 DealCardFromPack 方法。

此方法从牌堆中随机挑选一张牌，从牌堆中移除该牌并返回该牌。选择牌的逻辑不需要任何更改，但方法末尾从数组中检索牌的语句必须更新为改用 Dictionary 集合。此外，移除牌的代码（它现在已被发牌）也必须修改；你需要在列表中搜索该牌然后从列表中移除它。要定位该牌，请使用 Find 方法并指定一个查找具有匹配值的牌的谓词。谓词的参数应为 PlayingCard 对象（列表包含 PlayingCard 项）。

更新后的语句出现在第二个 while 循环的闭合大括号之后，如以下代码中加粗所示：

Click here to view code image

```
public PlayingCard DealCardFromPack()
{
    Suit suit = (Suit)randomCardSelector.Next(NumSuits);
    while (this.IsSuitEmpty(suit))
    {
        suit = (Suit)randomCardSelector.Next(NumSuits);
    }

    Value value = (Value)randomCardSelector.Next(CardsPerSuit);
    while (this.IsCardAlreadyDealt(suit, value))
    {
        value = (Value)randomCardSelector.Next(CardsPerSuit);
    }

    List<PlayingCard> cardsInSuit = this.cardPack[suit];
    PlayingCard card = cardsInSuit.Find(c => c.CardValue == value);
    cardsInSuit.Remove(card);
    return card;
}
```

## 10. 找到 IsCardAlreadyDealt 方法。

此方法通过检查数组中相应元素是否已设置为 null 来确定一张牌是否已被发牌。你需要修改此方法以确定 cardPack Dictionary 集合中花色对应的列表中是否存在指定值的牌。

要确定 List<T> 集合中是否存在项，可以使用 Exists 方法。此方法与 Find 类似，因为它也接受谓词作为参数。谓词会依次接收集合中的每个项，并应在其项匹配某些指定条件时返回 true，否则返回 false。在这种情况下，List<T> 集合保存 PlayingCard 对象，而 Exists 谓词的标准应返回 true，如果它接收到一个花色和值与传递给 IsCardAlreadyDealt 方法的参数匹配的 PlayingCard 项。

更新方法，如以下示例中加粗所示：

Click here to view code image

```
private bool IsCardAlreadyDealt(Suit suit, Value value)
{
    List<PlayingCard> cardsInSuit = this.cardPack[suit];
    return (!cardsInSuit.Exists(c => c.CardSuit == suit && c.CardValue == value));
}
```

11. 在代码和文本编辑器窗口中显示 Hand.cs 文件。向文件顶部的列表中添加以下 using 指令：

Click here to view code image

```
using System.Collections.Generic;
```

12. Hand 类当前使用名为 cards 的数组来保存手牌的扑克牌。将 cards 变量的定义修改为 List<PlayingCard> 集合，如此处加粗所示：

Click here to view code image

```
class Hand
{
    public const int HandSize = 13;
    private List<PlayingCard> cards = new List<PlayingCard>(HandSize);
    ...
}
```

13. 找到 AddCardToHand 方法。

此方法当前检查手牌是否已满；如果未满，它会将作为参数提供的牌添加到 cards 数组中 playingCardCount 变量指定的索引处。

更新此方法以改用 List<PlayingCard> 集合的 Add 方法。

此更改也消除了显式跟踪集合中牌数的必要性，因为你可以使用 cards 集合的 Count 属性。因此，从类中删除 playingCardCount 变量并修改检查手牌是否已满的 if 语句，使其引用 cards 集合的 Count 属性。

完成的方法应如下所示，其中更改以加粗突出显示：

Click here to view code image

```
public void AddCardToHand(PlayingCard cardDealt)
{
    if (this.cards.Count >= HandSize)
    {
        throw new ArgumentException("Too many cards");
    }
    this.cards.Add(cardDealt);
}
```

- 14. 在 Debug 菜单上，单击 Start Debugging 以构建并运行应用程序。
- 15. 当 Card Game 表单出现时，单击 Deal。

# Note

Deal 按钮位于命令栏上。你可能需要展开命令栏以显示该按钮。

验证牌是否已发牌并且填充的手牌如前所示。再次单击 Deal 以生成另一组随机手牌。
以下图像显示了正在运行的应用程序：

# Card Game

- North
- King of Diamonds
- Ten of Diamonds
- Four of Hearts
- Queen of Hearts
- Six of Hearts
- Five of Hearts
- Five of Clubs
- Jack of Diamonds
- Two of Spades
- Three of Diamonds
- Three of Hearts
- Ten of Spades
- King of Clubs

- South
- Ace of Spades
- Ace of Clubs
- Eight of Diamonds
- Ace of Hearts
- Six of Clubs
- Seven of Clubs
- Eight of Clubs
- Queen of Spades
- Four of Spades
- King of Hearts
- King of Spades
- Ten of Hearts
- Nine of Diamonds

- East
- Ace of Diamonds
- Jack of Spades
- Queen of Diamonds
- Nine of Hearts
- Ten of Clubs
- Six of Spades
- Two of Clubs
- Three of Spades
- Two of Diamonds
- Eight of Spades
- Jack of Hearts
- Two of Hearts
- Jack of Clubs

- West
- Five of Spades
- Nine of Clubs
- Seven of Hearts
- Seven of Diamonds
- Seven of Spades
- Five of Diamonds
- Four of Clubs
- Nine of Spades
- Six of Diamonds
- Eight of Hearts
- Three of Clubs
- Queen of Clubs
- Four of Diamonds

16. 返回 Visual Studio 2015 并停止调试。

# Summary

在本章中，你学习了如何使用一些常见的集合类来存储和访问数据。特别是，你学习了如何使用泛型集合类来创建类型安全的集合。你还学习了如何创建 lambda 表达式以在集合中搜索特定项。

- 如果你想继续下一章，请保持 Visual Studio 2015 运行并转到第 19 章，“Enumerating collections。”
- 如果你现在想退出 Visual Studio 2015，请在 File 菜单上单击 Exit。如果出现 Save 对话框，请单击 Yes 并保存项目。

# Quick reference

