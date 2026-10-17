
# 通用方法

```csharp
/**
* 目的：洗牌
* 参数列表:
* 无
* 返回值:
* int 洗牌所需的循环轮数
*/
public int ShuffleDeck() {
    int index;
    int val;
    Random rnd = new Random();
    passCount = 0; // 计算进入 while 循环的次数
    index = 1;
    Array.Clear(deck, 0, deck.Length); // 将数组初始化为 0
    while (index < deck.Length) {
        // 为从0开始的数组偏移 1
        val = rnd.Next(DECKSIZE) + 1; // 生成 1 到 52 之间的值
        if (deck[val] == 0) {
            // 这张牌在牌组中是否“未使用”？
            deck[val] = index; // 是，所以给它分配一个位置
            index++; // 为下一张牌准备
        }
        passCount++;
    }
    nextCard = 1; // 准备发第一张牌
    return passCount;
}
```

```csharp
/**
* 目的：显示牌组中指定的牌。
* 参数列表:
* int 牌的位置索引
* 返回值:
* string 牌的点数（pip），错误时返回空字符串
*/
public string getOneCard(int index)
{
    if (index > 0 && index <= deck.Length && nextCard <= deck.Length)
    {
        nextCard++;
        return pips[deck[index]];
    }
    else
    {
        return "";
    }
}
```

```csharp
/**
* 目的：显示牌组中指定牌的缩写。
* 参数列表:
* index 牌组中位置的整数索引
* 返回值:
* string 牌的点数（pip），错误时返回空字符串
*/
public string getCardPip(int index)
{
    if (index > 0 && index <= DECKSIZE)
    {
        return pips[index];
    }
    else
    {
        return "";
    }
}
```

现在检查类代码的每个部分。首先，注意到当你创建 `clsDeck` 时，Visual Studio 几乎将类封装在项目的命名空间 `namespace` 中。在第 9 章中由于相同的原因，从类中删除了命名空间。

# 类属性、构造函数和属性方法

属性的定义与图 10-2 完全一致。构造函数除了将 `nextCard` 的值设置为 1 之外没有进行其他操作。这样做是为了让牌组的第一张牌被视为 `deck[1]` 而不是 `deck[0]`。由于属性类型规定构造函数会将类属性初始化为 0，因此将 `nextCard` 初始化为 1。

# 设计与编写类

属性的 `setter` 方法用于确保数据的有效性。在设计洗牌逻辑时，我们需要通过循环来遍历牌组。

# 通用方法

在开发过程中，你经常会发现需要通用方法来处理逻辑。在 `clsDeck` 中，这些方法增强了代码的可复用性。

# ShuffleDeck 方法实现

为了理解发生的过程，当程序控制进入 `while` 循环且第一个随机数 `val` 分配 5 时，该语句检查 `deck[5]` 是否为 0。因为这是循环的第一次执行，`deck[5]` 是“空”的（即其值为 0），所以将 `index` 的值赋值给数组中的元素。由于变量 `index` 已经初始化为 1，牌组现在看起来像图 10-4。

# 洗牌算法实现

在 `while` 循环开始时，`deck` 数组看起来如图 10-3 所示。图显示没有任何元素被赋值。也就是说，图 10-3 中的每个空元素都是 0。

|  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Elements | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 50 | 51 | 52 |

**图 10-3：洗牌前的牌组状态**

为了理解正在发生的情况，当程序进入 `while` 循环且第一个随机数 `val` 分配 5 时，该语句检查 `deck[5]` 是否为 0。因为这是循环的第一次执行，`deck[5]` 是“空”的，所以将 `index` 的值赋值给数组中的元素。由于变量 `index` 已经初始化为 1，牌组现在看起来像图 10-4。

|  | 1 |  |  |  |  |  |  |  |  |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Elements | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 50 | 51 | 52 |

**图 10-4：添加第一张牌后的状态**

如果你查看之前讨论的 `pips` 数组，你应该会发现牌组中的第五张牌现在是黑桃 A。 在将 `index` 赋值给数组的 `deck[val]` 元素后，`index` 会递增。由于 `index` 的当前值等于 2，它小于数组元素的大小（在本例中为 53），因此会再次执行循环。

在循环的第二次执行中，假设下一个随机数是 51。由于元素 51 是 0（即“空”），所以 `if` 语句将值 2 赋值给 `deck[51]`。你现在知道黑桃 2 是牌组中的倒数第二张牌。此时牌组的状态如图 10-5 所示。

|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 50 | 51 | 52 |

图 10-5: 将卡牌加入牌组

在每次循环中，代码都会尝试使用 `val` 作为索引为 `deck` 数组中的空元素赋值。如果你仔细想一下，随着数组的填充，填充空数组会变得越来越困难。这就是为什么可能需要通过多次循环来用随机卡牌填满数组。`passCount` 变量记录了在 `deck` 数组填充之前循环执行的次数。通常，`deck` 数组在少于 300 次循环内即可填充。尽管目前有更高效的洗牌算法，但该代码的简单性和合理的速度使得这个版本可以满足你的需求。

当循环完成 `deck` 数组后，`nextCard` 被赋值为 1，且 `passCount` 的值被返回给调用者，如图 10-6 所示。

如果你在以下语句上设置断点：
`temp = myDeck.getOneCard(cardIndex);`

并在 `main` 方法的嵌套循环（第 10-5 行）中通过 F1 键进入 `getOneCard()` 方法，你可以看到卡牌是如何分配给列表对象的。再次强调，单步执行程序是理解其实际工作原理极佳方法。

## 使用 CLSCARDCK 设计卡牌游戏

现在你有了一个能够洗牌组牌并逐一发牌的类，请设计一个简单的卡牌游戏。这个游戏是 “In Between” 游戏的简化版。

这个游戏的变体是从庄家（计算机）给你 $100 用于赌注，默认注额为 $10。然后庄家会发两张朝上的牌。你可以对某局游戏不赌注，也可以赌掉你所有的余额。如果你不想投注，只需点击“发牌” `Deal` 再次来发另一组牌。

如果你下注，庄家会发下一张牌。如果那张牌落在前两张牌形成的范围内，你就赢了等于你注额的金额。你的收益会自动加入余额。如果第三张牌落在前两张牌的范围之外，你的余额将扣去注额金额。如果第三张牌与前两张牌中的任何一张相同，则庄家赢。A 在牌组中被视为最低值（1）和最高值（13）。

示例运行如图 10-6 所示。

例如，如果前两张牌是 6d 和 JS，第三张是 12s，那么玩家赢了，因为第三张牌（皇后，或 12）落在 6（六）到 11（Jack）的花色范围之外；庄家赢了，因为这些牌构成了平局，所以庄家平局。如果第三张牌落在 6 到 11 范围内，玩家赢。

## 使用 clsCardDeck 设计游戏

```csharp
int balance;
int position;
clsInBetweenRules myRules = new clsInBetweenRules();
string[] cards = new string[3];
private Button btnDeal;
private Button btnClose;
private Label label;
private TextBox txtBalance;
private Label lbl2;
private GroupBox groupBox1;
private Label lbl1low;
private Label lbl4;
private Label lbl3;
private TextBox txtH1;
private TextBox txtLow;
private Label lblLess;
private Label lblHi;
private Label lblMiddle;
private Button btnBet;
private Label lblOutcome;
private Button btnReset;
#region Windows code
public frm frmMain()
{
    bool flag;
    InitializeComponent();
    txtBalance.Text = myRules.Balance.ToString(); // 提取赌注
    txtWager.Text = myRules.Wager.ToString(); // 默认赌注 $10
    flag = int.TryParse(txtBalance.Text, out balance);
    flag = int.TryParse(txtWager.Text, out wager);
    myRules.Shuffle(); // 洗牌
}
public static void Main()
{
    frmMain main = new frmMain();
    Application.Run(main);
}
private void btnDeal_Click(object sender, EventArgs e)
{
    int retval;
    ClearRanges(); // 清除旧数据
    lblOutcome.Text = "*";
}
```

```csharp
retval = myRules.Balance;      // 剩余可投注的钱？？
if (retval == 0)
{
    MessageBox.Show("你破产了。游戏结束。");
    return;
}
retval = myRules.getCardsLeft();      // 剩余牌足够吗？？
if (retval < 3)
{
    lblOutcome.Text = "牌组已洗牌 . . ";
    myRules.Shuffle();
}
myRules.DealHand(cards, ref betResult, ref position);
ShowHiLow();
```

```csharp
private void btnWager_Click(object sender, EventArgs e)
{
    bool flag = int.TryParse(txtWager.Text, out wager);
    if (flag == false)
    {
        MessageBox.Show("仅限美元赌注。请重新输入。", "输入错误*");
        txtWager.Focus();
        return;
    }
    switch (betResult)
    {
        case TIE:
            lblOutcome.Text = "平局。庄家胜。";
            myRules.Balance = wager;
            break;
        case PLAYERWINS:
            lblOutcome.Text = "你赢了！";
            myRules.Balance += wager;
            break;
        case DEALERINS:
```

