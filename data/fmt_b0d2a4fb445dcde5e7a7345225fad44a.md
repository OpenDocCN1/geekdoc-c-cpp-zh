
| `void Populate()` `void Shuffle()` `void Deal(Hand&)` | 创建标准牌堆。洗牌。发牌到手牌。 |

| `AdditionalCards(GenericPlayer&)` | 给玩家额外的牌。 |

| 表 10.8 Game 类 |

| 成员 | 描述 |

| :--- | :--- |

| `Deck` `m_Deck` | 一副牌。 |

| `vector<Player>` `m_Players` | 人类玩家集合。 |

| `void Play()` | 进行黑色侍克游戏。 |

## 规划游戏

最后一部分是规划流程。这里是 `Game` 函数的一些伪代码：

- 发牌给玩家庄家

- 隐藏庄家的第一张牌

- 如果玩家爆牌

    输

- 如果玩家总分大于庄家总分

    赢

- 如果玩家总分小于庄家总分

    输

- 否则

## Card 类

在了一些初始语句之后，我为单张游戏牌定义了 `Card` 类。

```cpp
//黑色侍克
//一种简单的赌场游戏；适用于 1-7 名玩家
```

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
```

```cpp
#include <ctime>
```

```cpp
using namespace std;
class Card
public:
    enum rank (ACE=1, TWO, THREE, FOUR, FIVE, SIX, SEVEN, EIGHT, NINE, TEN,
    JACK, QUEEN, KING);
    enum suit (CLUBS, DIAMONDS, HEARTS, SPADES);
```

```cpp
//重载 operator << 让 Card 对象能够标准输出
friend ostream& operator<<=(ostream& os, const Card& aCard);
```

```cpp
Card(rank r = ACE, suit s = SPADES, bool if = true);
```

```cpp
//返回牌的值，1-11
int GetValue() const;
```

```cpp
//翻转牌：如果是正面则变为背朝，反之亦然
void Flip();
```

```cpp
private:
    rank m_Rank;
    suit m_Suit;
    bool m_IsFaceUp;
```

```cpp
Card::Card(rank r, suit s, bool if): m_Rank(r), m_Suit(s), m_IsFaceUp(if)
```

```cpp
int Card::GetValue() const
{
    //如果牌是背朝的，其值为 0
    int value = 0;
    if (m_IsFaceUp)
    {
        //正面显示的点数
        value = m_Rank;
        //人脸牌点数为 10
        if (value > 10)
```

```cpp
{
  value = 10;
}
return value;
n

void Card::Flip()
{
  m_IsFaceUp = !(m_IsFaceUp);
}
```

我定义了两个枚举 `rank`（点数）和 `suit`（花色），作为类成员变量 `m_Rank` 和 `m_Suit` 的类型。这样做有两个好处：首先，它让代码更具可读性。花色数据成员将拥有如 `CLUBS`（梅花）或 `HEARTS`（红心）的值，而不是 0 或 2。其次，它限制了这两个数据成员可以拥有的值。`m_Suit` 只能存储 `suit` 中的值，`m_Rank` 只能存储 `rank` 中的值。

接下来，我将重载的运算符 `<<()` 设置为类的友元函数，这样我就可以在屏幕上显示卡片对象。

`GetValue()` 返回 `Card` 对象的值，范围在 0 到 11 之间。王牌（Ace）的值为 11。（在 `Hand` 类中，我会根据手牌中的其他牌，考虑将它们计为 1 的情况）。背朝牌的值为 0。

## Hand 类

我定义了 `Hand` 类来管理卡牌集合。

```cpp
class Hand
{
public:
  Hand();

  virtual ~Hand();

// 向手牌中添加牌
void Add(Card* pCard);

// 清空手牌中的所有牌
void Clear();
```

## 第 10 章 = 继承与多态：黑 模式

```cpp
// 获取手牌总分，智能地将王牌计为 1 或 11
int GetTotal() const;

protected:
    vector<Card*> m_Cards;
};
```

```cpp
Hand::Hand()
{
    m_Cards.reserve(7);
}
```

```cpp
Hand::~Hand()
{
    Clear();
}
```

```cpp
void Hand::Add(Card* pCard)
{
    m_Cards.push_back(pCard);
}
```

```cpp
void Hand::Clear()
{
    // 遍历 vector，释放堆上的所有内存
    vector<Card*>::iterator iter = m_Cards.begin();
    for (iter = m_Cards.begin(); iter != m_Cards.end(); ++iter)
    {
        delete iter;
        *iter = 0;
    }
    // 清空指针 vector
    m_Cards.clear();
}
```

```cpp
int Hand::GetTotal() const
{
    // 如果手牌中为空，返回 0
    if (m_Cards.empty())
    {
        return 0;
    }

    // 如果第一张牌的值为 0，则牌是背朝的；返回 0
    if (m_Cards[0]->GetValue() == 0)
    {
        return 0;
    }

    // 相加卡牌值，将每张王牌计为 1
    int total = 0;
    vector<Card*>::const_iterator iter;
    for (iter = m_Cards.begin(); iter != m_Cards.end(); ++iter)
    {
        total += (*iter)->GetValue();
    }

    // 判断手牌是否包含王牌
    bool containsAce = false;
    for (iter = m_Cards.begin(); iter != m_Cards.end(); ++iter)
    {
        if ((*iter)->GetValue() == Card::ACE)
        {
            containsAce = true;
        }
    }

    // 如果手牌包含王牌且总分足够低，将王牌计为 11
    if (containsAce && total <= 11)
    {
        // 只加上 10，因为我们已经为王牌加过 1 了
        total += 10;
    }

    return total;
}
```

### 陷阱

类的析构函数是虚的（`virtual`），但注意我在实际定义析构函数时，没有在类外部使用 `virtual` 关键字。你只需要在类定义内部使用该关键字。别担心，析构函数仍然是虚的。

尽管我已经涵盖了这一点，但我想再次强调一下。所有的 `Card` 对象都存在于堆上。任何卡牌集合（作为 `Hand` 对象）都将拥有指向堆上的一组对象的指针 `vector`。

`Clear()` 成员函数承担着重要的责任。它不仅移除了 `mCards` vector 中的所有指针，还销毁了相关的 `Card` 对象并释放了它们占据的堆内存。这就像现实世界中的黑杰，当回合结束时卡牌会被丢弃。虚析构函数会调用 `Clear()`。

`GetTotal()` 成员函数返回手牌的总分。如果手牌包含王牌，它会被计为 1 或 11，以玩家最有利为准。程序通过检查手牌是否至少有一张王牌来实现这一点。如果是，它会检查将王牌计为 11 是否会导致手牌总分超过 21。如果不会，则将王牌计为 11。

## GenericPlayer 类

我定义 `GenericPlayer` 类是为了通用的黑杰玩家。它不代表具体的玩家。相反，它代表了共同元素。

```cpp
class GenericPlayer : Hand
{
    friend ostream& operator<<(ostream& os, const GenericPlayer& aGenericPlayer);
public:
    GenericPlayer(const string& name = "");
    virtual ~GenericPlayer();
    // 判断玩家是否要要牌
    virtual bool IsHitting() const = 0;
    // 玩家赢了
    virtual void Win() = 0;
    // 玩家输了
    virtual void Lose() = 0;
    // 玩家平局
    virtual void Push() = 0;
    // 判断玩家是否爆牌
    virtual bool IsBusted() const = 0;

protected:
    string m_Name;
};

GenericPlayer::GenericPlayer(const string& name)
{
    m_Name = name
}

GenericPlayer::~GenericPlayer()
{}

ostream& operator<<(ostream& os, const GenericPlayer& aGenericPlayer)
{
    os << aGenericPlayer.m_Name;
    return os;
}

bool GenericPlayer::IsBusted() const
{
    return GetTotal() > 21;
}

void GenericPlayer::Bust()
{
    cout << m_Name << " 爆牌了。\n";
}
```

## Player 类

`Player` 类代表玩家。它继承自 `GenericPlayer`。

```cpp
class Player : public GenericPlayer
{
public:
    Player(const string& name = "");

    virtual ~Player();

    // 判断玩家是否要牌
    bool IsHitting() const override;

    // 玩家赢了
    void Win() const override;

    // 玩家输了
    void Lose() const override;

    // 玩家平局
    void Push() const override;
};

Player::Player(const string& name)
{
    GenericPlayer(name)
}

Player::~Player()
{}

bool Player::IsHitting() const
{
    cout << m_Name << "，想再拿牌吗？(Y/N): ";
    char response;
    cin >> response;
    return (response == 'y' || response == 'Y');
}

void Player::Win() const
{
    cout << m_Name << " 赢了。\n";
}

void Player::Lose() const
{
    cout << m_Name << " 输了。\n";
}

void Player::Push() const
{
    cout << m_Name << " 平局。\n";
}
```

## House 类

`House` 类代表庄家。它继承自 `GenericPlayer`。

```cpp
class House : public GenericPlayer
{
public:
    House(const string& name = "House");

    virtual ~House();

    // 判断庄家是否要牌 - 在 16 点或以下时总是要牌
    virtual bool IsHitting() const override;

    // 翻开第一张牌
    void FlipFirstCard();
};

House::House(const string& name)
{
    GenericPlayer(name)
}

House::~House()
{}

bool House::IsHitting() const
{
    return GetTotal() <= 16;
}

void House::FlipFirstCard()
{
    // 此处应实现翻开第一张牌的逻辑
}
```

```cpp
House::House(const string& name):
  GenericPlayer(name)
{}
```

```cpp
House::~House()
{}
```

```cpp
bool House::IsHitting() const
{
  return (GetTotal() <= 16);
}
```

```cpp
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

该类实现了从 `GenericPlayer` 继承的 `IsHitting` 成员函数。因此，`House` 不是抽象类。该类通过调用 `GetTotal()` 实现该成员函数。如果返回值小于或等于 16，该成员函数返回 `true`，表示房屋仍在加牌；否则，返回 `false`，表示房屋不再加牌。

`FlipFirstCard()` 翻转房屋的第一张牌。这个成员函数是必要的，因为房屋在回合开始时会隐藏它的第一张牌，并在所有玩家都拿完所有额外牌后才将其揭开。

## The Deck Class

`Deck` 类代表一幅牌。它派自 `Hand`。

```cpp
class Deck : public Hand
{}
```

```cpp
public:
    Deck();

    virtual ~Deck();

    //创建一个 52 张牌的标准牌组
    void Populate();

    //洗牌
    void Shuffle();

    // 给手牌发一张牌
    void Deal(Hand&aHand);

    // 给通用玩家提供额外牌
    void AdditionalCards(GenericPlayer&aGenericPlayer);
};

Deck::Deck()
{
    m_Cards.reserve(52);
    Populate();
}

Deck::~Deck()
{}

void Deck::Populate(){
    Clear();
    // 创建标准牌组
    for (int s = Card::CLUBS; s <= Card::SPADES; ++s) {
        for (int r = Card::ACE; r <= Card::KING; ++r) {
            AddNewCard(static_cast<Card::rank>(r), static_cast<Card::suit>(s));
        }
    }
}

void Deck::Shuffle()
{
  random_shuffle(m_Cards.begin(), m_Cards.end());
}
```

```cpp
void Deck::Deal(Hand& aHand) {
  if (!m_Cards.empty()) {
    aHand.Add(m_Cards.back());
    m_Cards.pop_back();
  } else {
    cout << "Out of cards. Unable to deal.";
  }
}
```

```cpp
void Deck::AdditionalCards(GenericPlayer& aGenericPlayer) {
  cout << endl;
  // 只要通用玩家没有爆牌就继续发牌
  // 且他想再次加牌
  while (!aGenericPlayer.IsBusted() && aGenericPlayer.IsHitting()) {
    Deal(aGenericPlayer);
    cout << aGenericPlayer << endl;
    if (aGenericPlayer.IsBusted()) {
      aGenericPlayer.Bust();
    }
  }
}
```

## Type casting
