

## 第10章 ■ 继承与多态：Blackjack

你通过在函数头末尾放置等号和零来指定一个纯虚函数。这就是我在 Creature 中所做的，如下行所示：

```
virtual void Greet() const = 0;    //pure virtual member function
```

当一个类包含至少一个纯虚函数时，它就是一个抽象类。因此，Creature 是一个抽象类。我可以用它作为其他类的基类，但我不能从它实例化对象。

抽象类可以拥有数据成员和非纯虚的虚函数。在 Creature 中，我声明了一个数据成员 m_Health 和一个虚成员函数 DisplayHealth()。

### 从抽象类派生类

当你从抽象类派生一个新类时，你可以重写它的纯虚函数。如果你重写了它的所有纯虚函数，那么新类就不是抽象类，你可以从它实例化对象。当我从 Creature 派生 Orc 时，我用以下几行重写了 Creature 的一个纯虚函数：

```
void Orc::Greet() const
{
    cout << "The orc grunts hello.\n";
}
```

这意味着我可以从 Orc 实例化一个对象，这就是我在 main() 中用以下行所做的：

```
Creature* pCreature = new Orc();
```

代码在堆上实例化一个新的 Orc 对象，并将对象的内存位置赋给 pCreature，一个指向 Creature 的指针。即使我不能从 Creature 实例化对象，使用该类声明指针也是完全可以的。像所有基类指针一样，指向 Creature 的指针可以指向从 Creature 派生的任何类的对象，比如 Orc。

接下来，我用以下行调用 Greet()，即我在 Orc 中重写的纯虚函数：

```
pCreature->Greet();
```

正确的问候语 "The orc grunts hello." 被显示出来。最后，我调用在 Creature 中定义的 DisplayHealth()。

```
pCreature->DisplayHealth();
```

它也显示了正确的消息，"Health: 120"。

### 介绍 BLACKJACK 游戏

本章的最终项目是赌场纸牌游戏 Blackjack 的简化版本（不含俗气的绿色毛毡）。游戏规则如下：玩家被发下带有点数的牌。每位玩家试图达到总计 21 点而不超过该数。带数字的牌按面值计算。A 牌可算作 1 或 11（以对玩家最有利者为准），任何 J、Q 或 K 都算作 10。

电脑是庄家（赌场），它与一到七名玩家竞争。在回合开始时，所有参与者（包括庄家）都被发两张牌。玩家可以看到自己的所有牌以及总计。然而，庄家的一张牌暂时被隐藏。

接下来，每位玩家都有机会一次取一张额外牌，只要他喜欢就可以。如果玩家的总计超过 21（称为爆牌），玩家就输了。在所有玩家都有机会取额外牌后，庄家会揭示其隐藏的牌。庄家必须在总计为 16 或更少时继续取额外牌。如果庄家爆牌，所有未爆牌的玩家都获胜。否则，每个剩余玩家的总计与庄家的总计进行比较。如果玩家的总计大于庄家，他获胜。如果玩家的总计小于庄家，他输了。如果两个总计相同，玩家与庄家平局（也称为推牌）。图 10.6 显示了游戏。

![](img/34f09be0ed6217c465debc4490197d4f_379_0.png)

**Figure 10.6**

一名玩家获胜；另一名则运气不佳。

### 设计类

在开始使用多个类的项目编码之前，先在纸上绘制它们是有帮助的。你可以列出清单并包含每个类的简要描述。表 10.1 显示了我对 Blackjack 游戏的此类清单的第一次尝试。

为了简化，所有成员函数都将是 public，所有数据成员都将是 protected。此外，我只使用 public 继承，这意味着每个派生类都将继承其基类的所有成员。

**Table 10.1 Blackjack Classes**

| Class | Base Class | Description |
|---|---|---|
| Card | None | 一张 Blackjack 扑克牌。 |
| Hand | None | 一只 Blackjack 手牌。Card 对象的集合。 |
| Deck | Hand | 一副 Blackjack 牌组。具有 Hand 没有的额外功能，如洗牌和发牌。 |
| GenericPlayer | Hand | 一个通用的 Blackjack 玩家。不是完整的玩家，而是人类玩家和电脑玩家的共同元素。 |
| Player | GenericPlayer | 一名人类 Blackjack 玩家。 |
| House | GenericPlayer | 电脑玩家，庄家。 |
| Game | None | 一局 Blackjack 游戏。 |

除了用文字描述你的类外，绘制某种家族树来可视化你的类之间的关系也是有帮助的。这就是我在图 10.7 中所做的。

接下来，最好更具体一些。问问自己关于这些类的问题。它们到底代表什么？它们能做什么？它们如何与其它类协同工作？

![](img/34f09be0ed6217c465debc4490197d4f_380_0.png)

**Figure 10.7**

Blackjack 游戏类的继承层次结构。GenericPlayer 被着色，因为它最终成为一个抽象类。

我把 Card 对象看作是现实生活中的牌。你在从牌组发牌到手牌时不会复制一张牌；你移动它。对我来说，这意味着 Hand 将有一个数据成员，即指向 Card 对象的指针向量，这些对象存在于堆上。当一张牌从一个 Hand 移动到另一个 Hand 时，实际上是指针被复制和销毁。

我把玩家（人类玩家和电脑）看作是有名字的 Blackjack 手牌。这就是为什么我从 Hand 派生 Player 和 House（间接）。（另一种同样有效的做法是玩家拥有一只手牌。如果我走这条路，Player 和 House 将会有 Hand 数据成员而不是从 Hand 派生。）

我定义 GenericPlayer 来容纳 Player 和 House 共享的功能，而不是在两个类中重复此功能。

此外，我把牌组看作是与庄家分开的。牌组将以相同的方式向人类玩家和电脑控制的庄家发牌。这意味着 Deck 将有一个成员函数来发牌，该函数是多态的，可以与 Player 或 House 对象一起工作。

为了更详细地阐述，你可以列出你认为类将拥有的每个数据成员和成员函数，并附上每个的简要描述。这就是我在表 10.2 到 10.8 中接下来所做的。对于每个类，我只列出我在其中定义的内容。几个类当然会有从基类继承的成员。

**Table 10.2 Card Class**

| Member | Description |
|---|---|
| Rank m_Rank | 牌的点数（A、2、3 等）。rank 是所有 13 个点数的枚举。 |
| Suit m_Suit | 牌的花色（梅花、方块、红心或黑桃）。suit 是四种可能花色的枚举。 |
| bool m_IsFaceUp | 指示牌是否正面朝上。影响牌的显示方式和其价值。 |
| int GetValue() | 返回牌的价值。 |
| void Flip() | 翻转一张牌。正面朝上变为正面朝下，反之亦然。 |

**Table 10.3 Hand Class**

| Member | Description |
|---|---|
| vector<Card*> m_Cards | 牌的集合。存储指向 Card 对象的指针。 |
| void Add(Card* pCard) | 向手牌添加一张牌。向向量 m_Cards 添加指向 Card 的指针。 |
| void Clear() | 清除手牌中的所有牌。移除向量 m_Cards 中的所有指针，删除堆上所有关联的 Card 对象。 |
| int GetTotal() const | 返回手牌的总价值。 |

**Table 10.4 GenericPlayer Class (Abstract)**

| Member | Description |
|---|---|
| string m_Name | 通用玩家的姓名。 |
| virtual bool IsHitting() const = 0 | 指示通用玩家是否想要再要一张牌。纯虚函数。 |
| bool IsBusted() const | 指示通用玩家是否爆牌。 |
| void Bust() const | 宣布通用玩家爆牌。 |

**Table 10.5 Player Class**

| Member | Description |
|---|---|
| virtual bool IsHitting() const | 指示玩家是否想要再要一张牌。 |
| void Win() const | 宣布玩家获胜。 |
| void Lose() const | 宣布玩家输了。 |
| void Push() const | 宣布玩家平局。 |

