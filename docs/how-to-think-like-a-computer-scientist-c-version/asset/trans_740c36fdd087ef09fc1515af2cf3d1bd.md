
既然已经决定，我们就可以编写 `isGreater`。同样，参数（两张 `Card`）和返回类型（`boolean`）是显而易见的，而且我们需要在成员函数和非成员函数之间进行选择。这一次，参数是不对称的。我们是想知道“A 是否大于 B？”还是“B 是否大于 A？”，这很重要。因此，我认为将 `isGreater` 写成一个成员函数更有意义：

```
bool Card::isGreater(const Card& c2) const
{
    // 先检查花色
    if (suit > c2.suit) return true;
    if (suit < c2.suit) return false;

    // 如果花色相同，则检查点数
    if (rank > c2.rank) return true;
    if (rank < c2.rank) return false;

    // 如果点数也相同，返回 false
    return false;
}
```

然后我们调用它，从我们所提出的两个可能的问题的语法来看，这是显而易见的：

- Card1 (2, 11)
- Card2 (1, 11)

```
if (card1.isGreater(card2)) {
    card1.print();
    cout << "is greater than" << endl;
    card2.print();
}
```

你几乎可以像读英语一样读它：“如果 card1 大于 card2 ...”。这个程序的输出是

Jack of Hearts greater than
Jack of Diamonds

根据 `isGreater` 的逻辑，A（aces）小于 2（deuces）。作为一个练习，请修复它，让 A 的点大于 K（Kings），就像在大多数扑牌游戏中那样。

## 12.6 卡片向量 (Vectors of cards)

我选择 `Cards` 作为本章对象的，是因为卡片向量有一个显而易见的用途——一副牌。这里是创建一个包含 52 张新牌组的代码：

`apvector<Card> deck (52);`

这是该对象的状态图：

deck

| 0 | 1 | 2 | ... | 51 |
|---|---|---|---|---|
| suit: 0 | suit: 0 | suit: 0 | ... | suit: 0 |
| rank: 0 | rank: 0 | rank: 0 | ... | rank: 0 |

三个点代表我不喜欢画的那 48 张卡片。请记住，我们还没有初始化卡片的实例变量。在某些环境中，它们将被初始化为零（如图所示），但在其他环境中，它们可能包含任何可能的值。

初始化它们的一种方法是将一个 `Card` 作为第二个参数传递给构造函数：

`Card aceOfSpades (3, 1);`
`apvector<Card> deck (52, aceOfSpades);`

这段代码构建了一个包含 52 张完全相同卡片的牌组，就像是一副用于魔术表演的特殊牌。当然，构建一个包含 52 张不同卡片的牌组更有意义。为了做到这一点，我们使用嵌套循环。

外层循环从 0 到 3 枚举花色。对于每个花色，内层循环从 1 到 13 枚举点数。由于外层循环迭代 4 次，内层循环迭代 13 次，循环体总共执行 52 次（13 乘以 4）。

```
int i = 0;
for (int suit = 0; suit <= 3; suit++) {
  for (int rank = 1; rank <= 13; rank++) {
    deck[i].suit = suit;
    deck[i].rank = rank;
  }
  i++;
}
```

我使用了一个变量来跟踪下一张卡片应该放在的位置。注意，我们可以将选择数组元素的语法（`[]` 运算符）与从对象中选择实例变量的语法（`.` 运算符）组合起来。表达式 `deck[i].suit` 的意思是“牌组中第 i 张卡片的花色”。

## 12.7 printDeck 函数

作为一个练习，将这段构建牌组的代码封装在一个名为 `buildDeck` 的函数中，该函数不接受参数并返回一个完全填充的 `Cards` 向量。

每当你处理向量时，拥有一个包含向量内容的函数是非常方便的。我们已经见过好几次遍历向量的模式了，所以下面的函数应该读起来很熟悉：

```
void printDeck(const apvector<Card>& deck) {
  for (int i = 0; i < deck.length(); i++) {
    deck[i].print();
  }
}
```

到目前为止，大家并不意外我们可以将访问向量的语法与调用函数的语法组合起来。由于 `deck` 的类型是 `apvector<Card>`，`deck` 的元素类型是 `Card`。因此，在 `deck[i]` 上调用 `print` 是合法的。

## 12.8 搜索 (Searching)

我想写的下一个函数是搜索 `Cards` 向量，以检查它是否包含某个特定的卡片。这个函数为什么有用可能并不显而易见，但它给了我演示两种搜索方法：线性搜索和二分搜索（bisection search）。

线性搜索是两者中显而易见的：它遍历牌组并将每张卡片与我们要找的卡片进行比较。如果我们找到了，就返回卡片出现的索引。如果不在牌组中，我们返回 -1。

```
int find(const Card& card, const apvector<Card>& deck) {
  for (int i = 0; i < deck.length(); i++) {
    if (equals(deck[i], card)) return i;
  }
  return -1;
}
```

这个循环与 `printDeck` 中的循环完全相同。事实上，我写完程序后直接复制了它，这节省了我调试两次的麻烦。

在循环内部，我们将牌组的每个元素与 `card` 进行比较。函数一旦发现该卡片就会立即返回，这意味着如果我们找到了要找的卡片，就不需要遍历整个牌组。如果循环结束时没有找到该卡片，我们就知道卡片不在牌组中，并返回 -1。

为了测试这个函数，我写了以下代码：

```
apvector<Card> deck = buildDeck();

int index = card.find(deck[17]);
cout << "I found the card at index = " << index << endl;
```

代码的输出是

I found the card at index = 17

## 12.9 二分搜索 (Bisection search)

如果牌组中的卡片不是无序的，那么没有比线性搜索更快的搜索方法。我们必须查看每张卡片，否则无法确定我们想要的卡片是否不在。

当你在字典中查找单词时，你并不会线性地搜索每一个单词。原因是单词是按字母顺序排列的。结果是，你可能会使用一种类似于二分搜索的算法：

1. 从中间某个开始。
2. 选择页面上的一个单词并与你正在找的单词进行比较。
3. 如果找到了你要找的单词，停止。
4. 如果你要找的单词在页面单词之后，翻到字典中后面的某个部分并回到第 2 步。
5. 如果你要找的单词在页面单词之前，翻到字典中较的某个部分并回到第 2 步。

当你发现页面上有两个相邻的单词，而你的单词在它们之间时，你可以得出你的单词不在字典中的结论。唯一的可能是你的单词在某个地方被漏掉了，但这违背了我们关于单词按字母顺序排列的假设。

在牌组的情况下，如果我们知道卡片是有序的，我们可以写一个快得多的 `find` 版本。编写二分搜索最好的方法是使用递归函数。技巧是写一个名为 `bisect` 的函数，它接受两个参数 `low` 和 `high`，指示要搜索的向量段（包括 `low` 和 `high`）。

1. 为了搜索向量，在 `low` 和 `high` 之间选择一个索引，并称其为 `mid`。将 `mid` 处的卡片与你要找的卡片进行比较。
2. 如果找到了，停止。
3. 如果 `mid` 处的卡片比你的卡片大，在范围 `low` 到 `mid-1` 搜索。
4. 如果 `mid` 处的卡片比你的卡片小，在范围 `mid+1` 到 `high` 搜索。

步骤 3 和 4 看起来非常像递归调用。这里是这一切翻译成 C++ 的样子：

```
int findBect(const Card& card, const apvector<Card>& deck,
    int low, int high) {
    int mid = (high + low) / 2;
```

```
// 如果找到了卡片，返回它的索引
if (equals(deck[mid], card)) return mid;
```

```
// 否则，将卡片与中间卡片进行比较
if (deck[mid].isGreater(card)) {
    // 搜索牌组的前半部分
    return findBect(card, deck, low, mid-1);
} else {
    // 搜索牌组的后半部分
    return findBect(card, deck, mid+1, high);
}
```

这段代码包含了二分搜索的内核，它缺少了一部分。按照目前的写法，如果卡片不在牌组中，它将无限递归。我们需要一种检测这种条件并正确处理的方法（返回 -1）。

判断你的卡片不在牌组中最简单的方法是牌组中没有卡片，在 `high` 小于 `low` 时情况如此。当然，牌组中还有卡片，我的意思是 `low` 和 `high` 指定的牌组段中没有卡片。

加上那行后，函数就能正常工作了：

```
cout << low << " << " << high << endl;

if (high < low) return -1;

int mid = (high + low) / 2;
```
