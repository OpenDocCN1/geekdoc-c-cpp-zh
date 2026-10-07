
`lblOutcome.Text = "遗憾，你输了。";`

`myRules.Balance -= wager;`

`break;`

`}`

`txtWager.Text = myRules.Balance.ToString();`

`switch (position)`

`{`

`case 1:`

`lblIll.Text = cards[2];`

`break;`

`case 2:`

`lblLow.Text = cards[2];`

`break;`

`case 3:`

### 列表 10-7（续）

```csharp
lblMiddle.Text = cards[2];
break;
case 4:
lblHi.Text = cards[2];
break;
case 5:
lblMore.Text = cards[2];
break;
default:
MessageBox.Show("结果错误。", "处理错误");
break;
}
```

```csharp
private void ShowHiLow()
{
    txtLow.Text = cards[0];
    txtHi.Text = cards[1];
}
```

```csharp
private void ClearRanges()
{
    lblLess.Text = "";
    lblLow.Text = "";
    lblMiddle.Text = "";
    lblHi.Text = "";
    lblMore.Text = "";
}
```

```csharp
private void btnReset_Click(object sender, EventArgs e)
{
    myRules.Balance = 100;
    txtBalance.Text = "*100";
    txtWager.Text = "*10";
    ClearRanges();
}
```

```csharp
private void btnClose_Click(object sender, EventArgs e)
{
    Close();
}
```

构造函数中的代码初始化了 `clsBetweenRules` 类的文本框。当用户点击 `Deal`（发牌）按钮时，会调用几个方法。首先检查是检查玩家是否有足够的余额玩游戏。如果玩家破产，游戏将无法继续。用户可以点击 `Reset`（重置）按钮来重置初始余额。如果玩家有余额，程序会检查是否有足够的积分玩一手牌。如果没有，玩家将看到一条消息，说明牌组已洗牌且游戏继续。最后，牌局和两张牌将显示给庄家。如果你查看代码是如何工作的，此时赌注的结果已经确定了。牌局的结果仅取决于玩家是否点击 `Bet`（下注）按钮。

## 使用 `clsCardDeck` 设计纸牌游戏 | 285

### 使用 `ref` 关键字

如果玩家决定支付，`btnBet_Click()` 代码决定如何将结果显示给用户。当通过调用

`myRules.DealHand(cards, ref betResult, ref position);`

“发”牌时，变量 `Result` 决定了谁赢了赌注，变量 `position` 决定了第三张牌显示在五个标签中的哪个位置，如前所述。`cards` 变量是一个包含正在玩的三张牌的数组。由于 C# 方法只返回单个值，你无法使用简单的 `return` 语句返回调用所需的所有信息。相反，你传递 `betResult` 和 `position` 变量。`ref` 关键字出现在调用中的变量之前，C# 不会将变量的值传递给方法，但当使用 `ref` 关键字时，它告诉方法变量在内存中的“位置”，因此方法可以永久地更改变量的值。代码使用此机制永久地更改 `betResult` 和 `position` 的值。`btnBet_Click()` 方法中的两个 `switch` 语句使用这两个变量告知玩家赌注的结果。10-8 显示了 `clsBetweenRules` 类的代码。-列表 10-8：游戏代码 (`clsBetweenRules.cs`)

```csharp
using System;
class clsBetweenRules
{
    // 符号常量 = =========
    const int TIE = 0;
    const int PLAYERWINS = 1;
    const int DEALERS = 2;
    // 静态成员 = ==============
    private int balance; // 余额
    private int wager; // 当前赌注
    private int lowCard; // 低牌值
    private int lowIndex; // 此位置
    private int hiCard; // 高牌值
    private int hiCardIndex; // 此位置
    private int dealtCard; // 发出的牌值
    private clsCardDeck myDeck; // 牌组
    // 构造函数 = ==============
    public clsBetweenRules()
    {
        balance = 100;
        wager = 10;
        myDeck = new clsCardDeck();
    }
    // 属性方法 = =====
    public int Balance
    {
        get {
            return balance;
        }
        set {
            if (value >= 0) {
                balance = value;
            }
        }
    }
    public int Wager
    {
        get {
            return wager;
        }
        set {
            if (value > 0) {
                wager = value;
            }
        }
    }
    // 辅助方法 = ====================
    /**
     * 目的：发出下三张牌并填充
     * 从 frmMain 传递的数组。它总是将
     * 显示在 frmMain 上。
     * 参数列表：
     * string[] hand 一手的三张牌
     * 返回值：
     * void
     */
    private void SetCards(string[] hand)
    {
        int temp;
        hand[0] = myDeck.getCardPip(lowIndex);
        hand[1] = myDeck.getCardPip(hiCard);
        hand[2] = myDeck.getCardPip(dealtCard);
        if (lowCard == hiCard || lowCard < hiCard) // 平局
        {
            hand[0] = myDeck.getCardPip(lowIndex);
            hand[1] = myDeck.getCardPip(hiCard);
        }
        else
        {
            temp = hiCard; // 交换高牌和低牌
            hiCard = lowCard;
            lowCard = temp;
            temp = hiCardIndex; // 交换高低索引
            hiCardIndex = lowIndex;
            lowIndex = temp;
        }
        hand[0] = myDeck.getCardPip(lowCard);
        hand[1] = myDeck.getCardPip(hiCard);
    }
}
```

### 319

### 列表 10-8（续）

```csharp
wager = 10;
myDeck = new clsCardDeck();
}
```

### 320

### 使用 `clsCardDeck` 设计纸牌游戏

```csharp
int temp;
hand[0] = myDeck.getCardPip(lowIndex);
hand[1] = myDeck.getCardPip(hiCard);
hand[2] = myDeck.getCardPip(dealtCard);
if (lowCard == hiCard || lowCard < hiCard) // 平局
{
    hand[0] = myDeck.getCardPip(lowIndex);
    hand[1] = myDeck.getCardPip(hiCard);
}
else
{
    temp = hiCard; // 交换高牌和低牌
    hiCard = lowCard;
    lowCard = temp;
    temp = hiCardIndex; // 交换高低索引
    hiCardIndex = lowIndex;
    lowIndex = temp;
}
hand[0] = myDeck.getCardPip(lowCard);
hand[1] = myDeck.getCardPip(hiCard);
```

```csharp
+ *****
* 目的：设置赌注的结果并告诉在哪里显示
* 底朝牌。
+ * 参数列表：
* ref int Outcome 谁赢了游戏
* ref int position 放置底朝牌的位置
+ * 返回值：
* void
* 注意：这两个 int 是按引用传递的，这意味着
* 方法可以永久地更改它们的值。
```

```csharp
******
```

```csharp
private void SetWinnerAndPosition(ref int Outcome, ref int position)
{
    if (dealtCard == lowCard) // 发出的牌等于低牌
    {
        Outcome = DEALERINS;
        position = 2;
        return;
    }
    if (dealtCard < lowCard) // 发出的牌小于低牌
    {
        Outcome = DEALERW;
        position = 1;
        return;
    }
}
```

```cs
if (dealtCard > lowCard && dealtCard < hiCard) // 牌在范围内
{
    outCome = PLAYERINS;
    position = 3;
    return;
}
if (dealtCard == hiCard) // 发出的牌等于 hiCard
{
    outCome = DEALERINS;
    position = 4;
    return;
}
if (dealtCard > hiCard) // 发出的牌大于 hiCard
{
    outCome = DEALERINS;
    position = 5;
    return;
}
```

```cs
// ================= 普通方法 ============
* Purpose: 获取第一张牌并将其视为第一张显示的牌
* 参数列表:
* n/a
* 返回值:
* void
* 注意：K牌是一个特殊情况，因为它的模数为 0
*****
public void getFirstCard() {
    lowCardIndex = myDeck.getOneCard();
    lowCard = lowCardIndex % 13;
    if (lowCard == 0) // A King
        lowCard = 13;
}
```

```cs
/*
* Purpose: 获取第二张牌并将其视为第二张显示的牌
* 参数列表:
* n/a
* 返回值:
* void
* 注意：K牌是一个特殊情况，因为它的模数为 0
*****/
public void getSecondCard()
{
    hiCardIndex = myDeck.getOneCard();
    hiCard = hiCardIndex % 13;
    if (hiCard == 0) // A King
        hiCard = 13;
}
******
```

```cs
/**
* Purpose: 获取最后一张牌并将其视为底牌
* 参数列表:
* n/a
* 返回值:
* void
* 注意：K牌是一个特殊情况，因为模数为 0
*****/
public void getDealtCard()
{
    dealtCard = myDeck.getOneCard();
    dealtCard = dealtCardIndex % 13;
    if (dealtCard == 0) // A King
        dealtCard = 13;
}
******
```

```cs
/**
* Purpose: 洗牌
* own列表:
* n/a
* 返回值:
* void
******
public void Shuffle()
{
    myDeck.ShuffleDeck();
}
******
```

```cs
/**
* Purpose: 获取牌组中剩余牌数。
* 参数列表:
* n/a
* 返回值:
* int 剩余的牌数
* 注意：K牌是一个特殊情况，因为模数为 0
*****/
public int getCardsLeft()
{
    return myDeck.getCardsLeftInDeck();
}
```

# 列表 10-8（续）

```cs
/**
* Purpose: 发牌牌。注意所有三张牌都是一次性发出的，
* 发出的牌在下注之前不会显示。
* 结果在下注前就已经已知，但不会公开
*
* 参数列表:
* string[] hand 一手牌的三张牌
* ref int outCome 谁赢了游戏
* ref int position 显示底牌的位置
* 返回值:
* void
* 注意：这两个 int 类型是按引用传递的，这意味着该
* 方法可以永久地更改它们的值。
******
public void DealHand(string[] hand, ref int outCome, ref int position)
{
    getFirstCard(); // 获取前两张显示牌
    getSecondCard();
    getDealtCard(); // 获取底牌
    SetCards(hand); // 必要时重新排列
    // 设定胜者和显示底牌的位置
    SetWinnerAndPosition(ref outCome, ref position);
}
```

在列表 10-7 和 10-8 展示的代码中需要注意的一点是 `frmMain` 了 `clsCardDeck`。与牌组的所有交互由 `clsBetweenRules` 类管理，这本该如此。如果没有在牌组和玩家之间强制执行隔离，拉斯维斯的赌徒在发自己的牌时就会发生这种情况！为了适应游戏的需求，你可以在 `clsCard` 类中添加两个方法。这两个方法在列表 10-9 中所示。

# 列表 10-9：`getCard(clsCard.cs)` 的源代码

```cs
/**
* Purpose: 获取牌的索引。此方法
* 返回牌的字符串表示。
* 参数列表:
* void
* 返回值:
* int 数组中的索引，如果牌组中没有剩余牌则返回 0。
*/
public int getCard() {
    int nextCard++;
    if (nextCard <= DECKSIZE) {
        return deck[nextCard];
    } else {
        return 0;
    }
}
/**
* Purpose: 返回牌组中剩余牌的数量。
* 参数列表:
* void
* 返回值:
* int 牌组中剩余牌的数量。
*/
public int getCardsLeft() {
    return DECKSIZE;
