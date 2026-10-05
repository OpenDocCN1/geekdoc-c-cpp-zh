

7. 修改内部 for 循环中的代码，将新的 `PlayingCard` 对象添加到此集合中而不是数组中，如下代码中**加粗**部分所示：

点击此处查看代码图像

```
for (Suit suit = Suit.Clubs; suit <= Suit.Spades; suit++)
{
    List<PlayingCard> cardsInSuit = new List<PlayingCard>(CardsPerSuit);
    for (Value value = Value.Two; value <= Value.Ace; value++)
    {
        cardsInSuit.Add(new PlayingCard(suit, value));
    }
}
```

8. 在内部 for 循环之后，将 `List` 对象添加到 `cardPack` 字典中，并指定 `suit` 变量的值作为该项的键：

点击此处查看代码图像

```
for (Suit suit = Suit.Clubs; suit <= Suit.Spades; suit++)
{
    List<PlayingCard> cardsInSuit = new List<PlayingCard>(CardsPerSuit);
    for (Value value = Value.Two; value <= Value.Ace; value++)
    {
        cardsInSuit.Add(new PlayingCard(suit, value));
    }
    this.cardPack.Add(suit, cardsInSuit);
}
```

9. 找到 `DealCardPack` 方法。

此方法从牌组中随机抽取一张牌，从牌组中移除该牌并返回该牌。选择牌的逻辑不需要任何更改，但方法末尾从数组中检索牌的语句必须更新为使用字典。此外，从数组中移除牌（现已发出的牌）的代码必须进行修改；你需要在列表中搜索该牌并从列表中移除。找到 `Find` 方法并指定一个谓词来找到具有匹配值的牌。谓词的参数应该是一个 `PlayingCard` 对象（该列表包含 `PlayingCard` 项目）。

更新后的语句位于第二个 `while` 循环结束大括号之后，如下代码中**加粗**部分所示：

点击此处查看代码图像

```csharp
public PlayingCard DealCardFromPack() {
    Suit suit = (Suit)randomCardSelector.Next (NumSuits);
    while (this.IsSuitEmpty(suit)) {
        suit = (Suit)randomCardSelector.Next (NumSuits);
    }
    Value value = (Value)randomCardSelector.Next (CardsPerSuit);
    while (this.IsCardAlreadyDealt(suit, value)) {
        value = (Value)randomCardSelector.Next (CardsPerSuit);
    }
    List<PlayingCard> cardsInSuit = this.cardPack[suit];
    PlayingCard card = cardsInSuit.Find(c => c.CardValue == value);
    cardsInSuit.Remove(card);
    return card;
}
```

## 10. 定位 `IsCardAlreadyDealt` 方法。

此方法通过检查数组中相应的元素是否被设置为 `null` 来确定牌是否已经发出。你需要修改此方法，以确定 `cardPack` 字典集合中对应花色的列表中是否存在具有指定值的牌。

要确定 `List<T>` 集合是否存在某个项，你使用 `Exists` 方法。该方法与 `Find` 相似，它接受一个谓词作为参数，如果项目与集合中的每个项目匹配，则返回 `true`，否则返回 `false`。在这种情况下，`List<T>` 集合持有 `PlayingCard` 对象，如果传递的 `PlayingCard` 项目的花色和值与传递给 `IsCardAlreadyDealt` 方法的参数匹配，则 `Exists` 谓词的标准应返回 `true`。

更新该方法，如下例所示**加粗**部分：

点击此处查看代码图像

```csharp
private bool IsCardAlreadyDealt(Suit suit, Value value)
{
  List<PlayingCard> cardsInSuit = this.cardPack[suit];
  return (!cardsInSuit.Exists(c => c.CardSuit == suit &&
  c.Value == value));
}
```

- 11. 在代码和文本编辑器窗口中显示 `Hand.cs` 文件。在文件顶部添加以下 `using` 指令：

点击此处查看代码图像

```csharp
using System.Collections.Generic;
```

- 12. `Hand` 类目前使用一个名为 `cards` 的数组来存放手牌。修改 `cards` 变量的定义，使其成为 `List<PlayingCard>` 集合，并注释掉定义 `playingCardCount` 变量的语句，如下所示：

```csharp
class Hand
{
  public const int HandSize = 13;
  private List<PlayingCard> cards = new List<PlayingCard>(HandSize);
  // private int playingCardCount = 0;
}
```

`playingCardCount` 变量之前被用作手牌数组的索引。该变量现在不再需要了。

- 13. 找到 `AddCardTo` 方法。
此方法检查手牌是否已满；如果未满，则根据 `cards.playingCardCount` 变量指定的索引添加所提供的牌。更新此方法，以使用 `List<PlayingCard>` 集合的 `Add` 方法。
此更改还消除了显式跟踪集合中持有多少张牌的需求，因为你可以使用 `cards` 集合的 `Count` 属性。因此，从类中删除 `playingCardCount` 变量，并修改检查手牌是否已满的 `if` 语句以引用 `cards` 集合的 `Count` 属性。

完成后的方法应如下（包含了更改）：

```csharp
public void AddCardTo(PlayingCard dealt)
{
    if (cards.Count >= HandSize)
    {
        throw new ArgumentException("Hand is full");
    }
    cards.Add(dealt);
}
```

- 14. [OCR 识别内容缺失]
- 15. [OCR 识别内容缺失]
- 16. [OCR 识别内容缺失]

