
```csharp
// return string representation of Card
public override string ToString() => $"{Face} of {Suit}";
}
```

图 8.10 | Card 类表示一张扑克牌。（第 2 部分，共 2 部分。）

构造函数（第 9–13 行）接收两个字符串，并用它们初始化该类的属性。方法 `ToString`（第 16 行）——此处实现为表达式主体方法——创建一个由牌的 `Face`、字符串 `" of "` 和牌的 `Suit` 组成的字符串（例如 `"Ace of Spades"`）。当对象用在需要字符串的地方时，对象的 `ToString` 方法会在许多情况下被隐式调用，例如

-   当 `Write` 或 `WriteLine` 输出该对象时，
-   当使用 `+` 运算符将该对象连接到字符串时，或
-   当将该对象插入字符串插值表达式时。

也可以显式调用 `ToString` 来获取对象的字符串表示形式。必须使用与图 8.10 第 16 行所示完全相同的标头来声明 `ToString`。我们将在第 11.4.1 节解释 `override` 关键字的用途。

## 8.6.2 DeckOfCards 类

`DeckOfCards` 类（图 8.11）创建并管理一个 `Card` 引用的数组。命名常量 `NumberOfCards`（第 10 行）指定一副牌中 `Cards` 的数量（52）。第 11 行声明一个名为 `deck` 的实例变量，它引用一个包含 `NumberOfCards`（52）个元素的 `Card` 对象数组——`deck` 数组的元素默认是 `null`。与简单类型数组变量的声明类似，对象数组变量的声明（例如 `Card[] deck`）包含数组元素的类型，后跟方括号和数组变量名。`DeckOfCards` 类还声明了 `int` 实例变量 `currentCard`（第 12 行），表示要从 `deck` 数组中发出的下一张 `Card`。注意，我们不能对 `NumberOfCards`、`deck` 和 `currentCard` 使用 `var` 进行类型推断，因为它们不是方法或属性的局部变量。

```csharp
// Fig. 8.11: DeckOfCards.cs
// DeckOfCards class represents a deck of playing cards.
using System;

class DeckOfCards
{
    // create one Random object to share among DeckOfCards objects
    private static Random randomNumbers = new Random();

    private const int NumberOfCards = 52; // number of cards in a deck
    private Card[] deck = new Card[NumberOfCards];
    private int currentCard = 0; // index of next Card to be dealt (0-51)
```

图 8.11 | DeckOfCards 类表示一副扑克牌。（第 1 部分，共 2 部分。）

```csharp
    // constructor fills deck of Cards
    public DeckOfCards()
    {
        string[] faces = {"Ace", "Deuce", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Jack", "Queen", "King"};
        string[] suits = {"Hearts", "Diamonds", "Clubs", "Spades"};

        // populate deck with Card objects
        for (var count = 0; count < deck.Length; ++count)
        {
            deck[count] = new Card(faces[count % 13], suits[count / 13]);
        }
    }

    // shuffle deck of Cards with one-pass algorithm
    public void Shuffle()
    {
        // after shuffling, dealing should start at deck[0] again
        currentCard = 0; // reinitialize currentCard

        // for each Card, pick another random Card and swap them
        for (var first = 0; first < deck.Length; ++first)
        {
            // select a random number between 0 and 51
            var second = randomNumbers.Next(NumberOfCards);

            // swap current Card with randomly selected Card
            Card temp = deck[first];
            deck[first] = deck[second];
            deck[second] = temp;
        }
    }

    // deal one Card
    public Card DealCard()
    {
        // determine whether Cards remain to be dealt
        if (currentCard < deck.Length)
        {
            return deck[currentCard++]; // return current Card in array
        }
        else
        {
            return null; // indicate that all Cards were dealt
        }
    }
}
```

图 8.11 | DeckOfCards 类表示一副扑克牌。（第 2 部分，共 2 部分。）

### DeckOfCards 类：构造函数

构造函数（第 22–25 行）用 `Cards` 填充 `deck` 数组。`for` 语句将 `count` 初始化为 0，并在 `count` 小于 `deck.Length` 时循环，使 `count` 依次取 0 到 51 的每个整数值（即 `deck` 数组的索引）。每个 `Card` 都用两个字符串初始化——一个来自第 17–18 行的 `faces` 数组（包含 `"Ace"` 到 `"King"`），另一个来自第 19 行的 `suits` 数组（包含 `"Hearts"`、`"Diamonds"`、`"Clubs"` 和 `"Spades"`）。计算 `count % 13`（第 24 行）的结果为 0 到 12 的值——即数组 `faces` 的 13 个索引。类似地，计算 `count / 13` 的结果始终为 0 到 3 的值——即数组 `suits` 的四个索引。当 `deck` 数组初始化时，它包含按每种花色顺序排列的、牌面为 `"Ace"` 到 `"King"` 的 `Cards`。注意，在第 22–25 行不能使用 `foreach` 循环，因为我们需要修改 `deck` 的每个元素。

### DeckOfCards 类：Shuffle 方法

`Shuffle` 方法（第 29–45 行）对 `deck` 中的 `Cards` 进行洗牌。该方法循环遍历全部 52 张 `Cards`，并执行以下任务：

-   对每张 `Card`，选取 0 到 51 之间的一个随机数来选择另一张 `Card`。
-   接着，交换当前 `Card` 对象和随机选中的 `Card` 对象。这个交换由第 41–43 行的三条赋值语句完成。额外变量 `temp` 临时存储被交换的两个 `Card` 对象之一。

*仅用下面两条语句无法完成交换*

```csharp
deck[first] = deck[second];
deck[second] = deck[first];
```

如果 `deck[first]` 是 `"Spades"` 的 `"Ace"`，而 `deck[second]` 是 `"Hearts"` 的 `"Queen"`，那么在第一次赋值后，两个数组元素都包含 `"Hearts"` 的 `"Queen"`，而 `"Spades"` 的 `"Ace"` 丢失了——因此需要额外变量 `temp`。`for` 循环终止后，`Card` 对象按随机顺序排列。在一次遍历整个数组的过程中只进行 52 次交换，`Card` 对象数组就完成了洗牌。

### 建议：使用无偏洗牌算法

建议在真实纸牌游戏中使用所谓的无偏洗牌算法。这种算法确保所有可能的洗牌后牌序出现的概率相等。一种流行的无偏洗牌算法是 Fisher-Yates 算法

http://en.wikipedia.org/wiki/Fisher-Yates_shuffle

该网页还使用伪代码展示如何实现该算法。

### DeckOfCards 类：DealCard 方法

`DealCard` 方法（第 48–59 行）发一张 `Card`。回想一下，`currentCard` 表示牌堆顶部 `Card` 的索引。因此，第 51 行将 `currentCard` 与 `deck` 数组的长度进行比较。如果牌堆不为空（即 `currentCard` 小于 52），第 53 行返回顶部 `Card` 并递增 `currentCard`，为下一次调用 `DealCard` 做准备——否则，第 57 行返回 `null`，表示已经到达牌堆末尾。

## 8.6.3 洗牌与发牌

图 8.12 演示了 `DeckOfCards` 类（图 8.11）的洗牌和发牌功能。图 8.12 的第 10 行创建一个名为 `myDeckOfCards` 的 `DeckOfCards` 对象，并使用类型推断确定该变量的类型。回想一下，`DeckOfCards` 构造函数按花色和牌面顺序创建包含 52 个 `Card` 对象的牌堆。第 11 行调用 `myDeckOfCards` 的 `Shuffle` 方法重新排列 `Card` 对象。第 14–22 行的 `for` 语句发出牌堆中的全部 52 张 `Cards`，并将它们按每行 13 张、共四列显示。第 16 行通过调用 `myDeckOfCards.DealCard` 方法发出一张并显示一个 `Card` 对象。当 `Card` 对象放入字符串插值表达式时，会隐式调用 `Card` 的 `ToString` 方法。由于字段宽度为负数，结果显示在宽度为 19 的字段中并左对齐。

```csharp
1  // Fig. 8.12: DeckOfCardsTest.cs
2  // Card-shuffling-and-dealing app.
3  using System;
4
5  class DeckOfCardsTest
6  {
7     // execute app
8     static void Main()
9     {
10       var myDeckOfCards = new DeckOfCards();
11       myDeckOfCards.Shuffle(); // place cards in random order
12
13       // display all 52 Cards in the order in which they are dealt
14       for (var i = 0; i < 52; ++i)
15       {
16          Console.Write($"{myDeckOfCards.DealCard(),-19}");
17
18          if ((i + 1) % 4 == 0)
19          {
20             Console.WriteLine();
21          }
22       }
23    }
24  }
```

|  |  |  |  |
|---|---|---|---|
| 梅花8 | 梅花10 | 黑桃10 | 黑桃4 |
| 黑桃A | 黑桃J | 黑桃3 | 黑桃7 |
| 方块3 | 红桃5 | 黑桃8 | 梅花5 |
| 红桃A | 红桃10 | 红桃2 | 梅花2 |
| 红桃J | 黑桃9 | 红桃4 | 梅花7 |
| 黑桃Q | 方块7 | 方块5 | 梅花A |
| 梅花4 | 方块10 | 梅花J | 方块6 |
| 方块8 | 红桃K | 梅花3 | 黑桃K |
| 方块K | 黑桃6 | 黑桃2 | 黑桃5 |
| 梅花Q | 梅花K | 红桃Q | 红桃7 |
| 方块A | 方块2 | 方块4 | 梅花9 |
| 方块Q | 方块J | 红桃6 | 方块9 |
| 红桃9 | 红桃3 | 梅花6 | 红桃8 |

图 8.12 | 洗牌与发牌应用。

## 8.7 将数组和数组元素传递给方法

要将数组实参传递给方法，请指定数组名，*不带任何方括号*。例如，如果 `hourlyTemperatures` 声明为

```csharp
var hourlyTemperatures = new double[24];
```

