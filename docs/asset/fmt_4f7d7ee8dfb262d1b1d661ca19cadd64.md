
```csharp
static void PerformSingleSwap(List<Card> cards, int index)
{
  int randomIndex = rand.Next(1, cards.Count);
  Card firstCard = cards[index];
  Card randomCard = cards[randomIndex];
  cards[index] = randomCard;
  cards[randomIndex] = firstCard;
}
```

# 第 23 章. 问题解决方法

```csharp
static void ShuffleCards(List<Card> cards)
{
    for (int i = 0; i < cards.Count; i++) {
        PerformSingleSwap(cards, i);
    }
}
```

我们执行程序，得到了对 52 张牌更的洗牌结果：

- (9 HEART)(5 CLUB)(3 CLUB)(7 SPADE)(6 CLUB)(5 SPADE)(6 HEART)(4 HEART)(10 CLUB)(3 SPADE)(K DIAMOND)(10 HEART)(8 CLUB)(A CLUB)(J DIAMOND)(K SPADE)(9 SPADE)(7 CLUB)(10 DIAMOND)(9 DIAMOND)(8 HEART)(6 CLUB)(5 SPADE)(4 HEART)(10 SPADE)(J CLUB)(Q SPADE)(9 CLUB)(J HEART)(K CLUB)(2 HEART)(7 HEART)(A HEART)(3 HEART)(K HEART)(8 DIAMOND)(4 SPADE)(5 HEART)(Q HEART)(4 DIAMOND)(2 SPADE)(A DIAMOND)(2 SPADE)(7 DIAMOND)(Q DIAMOND)(2 CLUB)(Q CLUB)

看起来在程序每次执行时，牌最终都是随机排列的。我们没有看到任何 bug（即重复或缺失的牌，或者处于相同位置的牌）。程序运行很快，而且它不会休眠。看起来我们表现得很好。

让我们看看另一个任务：数字排序。什么是严重的常见情况测试？对我们来说，生成 100 个甚至 1000 个随机数并对其排序很容易。检查最终答案是否正确也很：数字必须按大小排序。另一个很好的测试是按降序输入 1 到 1000 的数字。输出也必须包含 1000 个数字，但必须是升序的。我们可以说，最困难的测试是检查我们的程序是否能处理许多数字——那么我们就可以说我们的程序运行正常。

让我们看看在解决编程问题时必须考虑的其他类型的测试。

## 边界情况 (Borderline Cases)

我们在解决问题时经常错过的一步是测试边界情况。当输入数据处于正常情况与最可能不会发生的情况之间的边界时，就会发生边界情况。在这种情况下，程序会崩溃，因为没有考虑非常大或非常小的数据量，尽管这些数据是有可能输入的。这显然是程序员的错，因为他没有想过这种情况可能会发生。

## C# 计算机编程基础

如何想出边界情况？我们分析输入到程序的所有数据，并想出可能输入的极端值。这些值可能极小、极大，或者只是很奇怪。如果说上限是 52，那么 52 左右的值也都是边界值，并可能导致错误。

## 边界情况：洗牌一张牌

在我们的洗牌程序中，一个边界问题是只洗牌一张牌。这种情况是完全有效的（尽管不寻常），但我们的程序可能无法正确处理它。让我们看看如果输入一副只有牌牌会发生什么。我们可以编写如下测试：

```csharp
static void TestOneCard()
{
    List<Card> cards = new List<Card>();
    cards.Add(new Card() { Face = "A", Suit = Suit.CLUB });
    CardsShuffle.Shuffle(cards);
    CardsShuffle.PrintCards(cards);
}
```

我们执行程序并得到了一个意想不到的结果：

Unhandled Exception: System.ArgumentRangeException: Index was out of range. Must be non-negative and less than the size of the collection. Parameter name: index

at System.ThrowArgumentRangeException(Object argument, Object resource)

at System.ThrowArgumentRangeException()

at System.Collections.Generic.List`1.Item(Int32 index)

at CardsShuffle.PerformSingleSwap(List`1 cards, Int32 index) 

D:\Projects\CardsShuffle.cs:line 61

错误发生是因为传递给生成随机数方法的参数是非法的。我们的程序可以处理正常的扑牌，但不能处理只有一张牌的扑牌。我们发现了一个简单的修复方法，这个 bug 是可以修复的：

```csharp
static void ShuffleCards(List<Card> cards)
{
    if (cards.Count > 1)
    {
        for (int i = 0; i < cards.Count; i++)
        {
            PerformSingleSwap(cards, i);
        }
    }
}
```

我们再次执行程序，得到了一个更好的对 52 张牌的洗牌结果：

- (9 HEART)(5 CLUB)(3 CLUB)(7 SPADE)(6 CLUB)(5 SPADE)(6 HEART)(4 HEART)(10 CLUB)(3 SPADE)(K DIAMOND)(10 HEART)(8 CLUB)(A CLUB)(J DIAMOND)(K SPADE)(9 SPADE)(7 CLUB)(10 DIAMOND)(9 DIAMOND)(8 HEART)(6 CLUB)(5 SPADE)(4 HEART)(10 SPADE)(J CLUB)(Q SPADE)(9 CLUB)(J HEART)(K CLUB)(2 HEART)(7 HEART)(A HEART)(3 HEART)(K HEART)(8 DIAMOND)(4 SPADE)(5 HEART)(Q HEART)(4 DIAMOND)(2 SPADE)(A DIAMOND)(2 SPADE)(7 DIAMOND)(Q DIAMOND)(2 CLUB)(Q CLUB)

看起来在程序每次执行时，牌最终都是随机排列的。我们没有看到任何 bug（即重复或缺失的牌，或者处于相同位置的牌）。程序运行很快，而且它不会休眠。看起来我们表现得很好。
