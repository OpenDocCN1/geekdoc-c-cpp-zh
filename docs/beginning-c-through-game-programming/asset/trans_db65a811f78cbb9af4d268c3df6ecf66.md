
```
void Creature::DisplayHealth() const
{
    cout << "Health: " << m_Health << endl;
}

class Orc : public Creature
{
public:
    Orc(int health = 120);
    virtual void Greet() const;
};

Orc::Orc(int health):
    Creature(health)
{}

void Orc::Greet() const
{
    cout << "The orc grunts hello.\n";
}

int main()
{
    Creature* pCreature = new Orc();
    pCreature->Greet();
    pCreature->DisplayHealth();

    return 0;
}
```

## 声明纯虚函数

纯虚函数是指不需要给出定义的函数。其背后的逻辑是，在类中可能没有该成员函数的良好定义。例如，我认为在我的 Creature 类中定义 Greet() 函数没有意义，因为问候真的取决于生物的具体类型——仙子闪烁，龙吹出一口烟，而兽人咕哝。

![](img/c7e8651578bccd573227f684823b8754_379_0.png)

## 图 10.6

一名玩家获胜；另一名则运气不佳。

## 表 10.1 Blackjack 类

| 类 | 基类 | 描述 |
|---|---|---|
| Card | None | 一张 Blackjack 扑克牌。 |
| Hand | None | 一副 Blackjack 手牌。Card 对象的集合。 |
| Deck | Hand | 一副 Blackjack 牌堆。具有 Hand 不具备的额外功能，例如洗牌和发牌。 |
| GenericPlayer | Hand | 通用的 Blackjack 玩家。不是完整的玩家，而是人类玩家和电脑玩家的共同元素。 |
| Player | GenericPlayer | 人类 Blackjack 玩家。 |
| House | GenericPlayer | 电脑玩家，即庄家。 |
| Game | None | 一局 Blackjack 游戏。 |

除了用文字描述你的类之外，画一个类似家谱的东西来可视化类之间的关系会有所帮助。这就是我在图 10.7 中所做的。

![](img/c7e8651578bccd573227f684823b8754_380_0.png)

图 10.7
Blackjack 游戏类的继承层次结构。`GenericPlayer` 被着色，因为它最终是一个抽象类。

我把 `Card` 对象看作是现实生活中的卡片。当你从牌堆发牌到手牌时，你不会复制一张卡片；你移动它。对我来说，这意味着 `Hand` 将有一个数据成员，即指向 `Card` 对象的指针向量，这些对象存在于堆上。当一张卡片从一个 `Hand` 移动到另一个 `Hand` 时，实际上是指针被复制和销毁。

我把玩家（人类玩家和电脑）看作是有名字的 Blackjack 手牌。这就是为什么我从 `Hand` 派生 `Player` 和 `House`（间接）。（另一种同样有效的观点是玩家拥有手牌。如果我采用这种方式，`Player` 和 `House` 将拥有 `Hand` 数据成员，而不是从 `Hand` 派生。）

我定义 `GenericPlayer` 来容纳 `Player` 和 `House` 共享的功能，而不是在两个类中重复此功能。

此外，我把牌堆看作是与庄家分离的。牌堆将以相同的方式向人类玩家和电脑控制的庄家发牌。这意味着 `Deck` 将有一个发牌的成员函数，该函数是多态的，可以与 `Player` 或 `House` 对象一起工作。

为了更详细地阐述，你可以列出你认为类将具有的数据成员和成员函数，并附上每个的简要描述。这就是我在表 10.2 到 10.8 中接下来要做的事情。对于每个类，我只列出我在其中定义的内容。几个类当然会有来自基类的继承成员。

### 表 10.2 Card 类

| 成员 | 描述 |
|---|---|
| rank m_Rank | 卡片的点数（A、2、3 等）。rank 是所有 13 种点数的枚举。 |
| suit m_Suit | 卡片的花色（梅花、方块、红心或黑桃）。suit 是四种可能花色的枚举。 |
| bool m_IsFaceUp | 指示卡片是否正面朝上。影响卡片的显示方式及其价值。 |
| int GetValue() | 返回卡片的值。 |
| void Flip() | 翻转一张卡片。正面朝上变为正面朝下，反之亦然。 |

### 表 10.3 Hand 类

| 成员 | 描述 |
|---|---|
| vector<Card*> m_Cards | 卡片集合。存储指向 Card 对象的指针。 |
| void Add(Card* pCard) | 向手牌添加一张卡片。向向量 m_Cards 添加指向 Card 的指针。 |
| void Clear() | 清空手牌中的所有卡片。移除向量 m_Cards 中的所有指针，删除堆上所有关联的 Card 对象。 |
| int GetTotal() const | 返回手牌的总价值。 |

### 表 10.4 GenericPlayer 类（抽象）

| 成员 | 描述 |
|---|---|
| string m_Name | 通用玩家的名字。 |
| virtual bool IsHitting() const = 0 | 指示通用玩家是否想要再要一张牌。纯虚函数。 |
| bool IsBusted() const | 指示通用玩家是否爆牌。 |
| void Bust() const | 宣布通用玩家爆牌。 |

### 表 10.5 Player 类

| 成员 | 描述 |
|---|---|
| virtual bool IsHitting() const | 指示玩家是否想要再要一张牌。 |
| void Win() const | 宣布玩家获胜。 |
| void Lose() const | 宣布玩家失败。 |
| void Push() const | 宣布玩家平局。 |

```
#include <ctime>

using namespace std;
class Card
{
public:
    enum rank {ACE = 1, TWO, THREE, FOUR, FIVE, SIX, SEVEN, EIGHT, NINE, TEN,
        JACK, QUEEN, KING};
    enum suit {CLUBS, DIAMONDS, HEARTS, SPADES};

//overloading << operator so can send Card object to standard output
friend ostream& operator<<(ostream& os, const Card& aCard);

Card(rank r = ACE, suit s = SPADES, bool ifu = true);

//returns the value of a card, 1 - 11
int GetValue() const;

//flips a card; if face up, becomes face down and vice versa
void Flip();

private:
    rank m_Rank;
    suit m_Suit;
    bool m_IsFaceUp;
};

Card::Card(rank r, suit s, bool ifu): m_Rank(r), m_Suit(s), m_IsFaceUp(ifu)
{}

int Card::GetValue() const
{
    //if a cards is face down, its value is 0
    int value = 0;
    if (m_IsFaceUp)
    {
        //value is number showing on card
        value = m_Rank;
        //value is 10 for face cards
        if (value > 10)
```
```
//gets hand total value, intelligently treats aces as 1 or 11
int GetTotal() const;

protected:
    vector<Card*> m_Cards;
};

Hand::Hand()
{
    m_Cards.reserve(7);
}

Hand::~Hand()
{
    Clear();
}

void Hand::Add(Card* pCard)
{
    m_Cards.push_back(pCard);
}

void Hand::Clear()
{
    //iterate through vector, freeing all memory on the heap
    vector<Card*>::iterator iter = m_Cards.begin();
    for (iter = m_Cards.begin(); iter != m_Cards.end(); ++iter)
    {
        delete *iter;
        *iter = 0;
    }
    //clear vector of pointers
    m_Cards.clear();
}

int Hand::GetTotal() const
{
    //if no cards in hand, return 0
    if (m_Cards.empty())
    {
        return 0
```

该图像包含一个文档编辑界面的用户界面截图。可见的主要文档内容大部分不完整、不清晰，无法可靠提取。

部分可见的手写风格文本和绘图元素存在，但模糊且无法阅读。

```
House::House(const string& name):
    GenericPlayer(name)
{}
```

```
House::~House()
{}
```

```
bool House::IsHitting() const
{
    return (GetTotal() <=16);
}
```

```
void House::FlipFirstCard()
{
    if (!m_Cards.empty())
    {
        m_Cards[0]->Flip();
    }
    else
    {
        cout << "No card to flip!\n";
    }
}
```

该类实现了从 GenericPlayer 继承的 IsHitting() 成员函数。因此，House 不是抽象的。该类通过调用 GetTotal() 来实现该成员函数。如果返回的总值为 16 或更小，则成员函数返回 true，表示庄家仍在要牌。否则，它返回 false，表示庄家不再要牌。

FlipFirstCard() 翻转庄家的第一张卡片。此成员函数是必要的，因为庄家在回合开始时隐藏其第一张卡片，然后在所有玩家都拿完所有额外卡片后才揭示它。

## Deck 类

Deck 类表示一副牌。它派生自 Hand。

```
class Deck : public Hand
{
```
