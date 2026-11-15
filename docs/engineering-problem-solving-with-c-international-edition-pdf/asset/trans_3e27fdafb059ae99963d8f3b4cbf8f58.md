

从一副牌中抽取 2 张卡片的实验重复 $n$ 次，并统计事件 $E$ 发生的次数 $n_E$。分数 $n_E/n$ 是衡量 $E$ 发生可能性的指标。我们的直觉告诉我们，如果进行两次该实验（$n=2$），$n_E$ 最可能为零。然而，如果进行一万次该实验（$n=10,000$），$n_E$ 最可能大于零。因此，$P(E)$ 表示一个数，即 $n_E/n$，当 $n$ 变得非常大时。

要估计从一副 52 张的牌中抽取 2 张 K 的概率，我们可以手动进行 $n$ 次实验并统计事件发生的次数，也可以编写模拟程序进行 $n$ 次实验并报告结果。无论哪种情况，我们都在统计概率实验的结果，且结果会有所不同。概率论使用基于集合论的公式来计数结果并计算概率。

假设我们有一个包含 $n$ 个元素的集合 $S$，并且选择 $r$ 使得 $1 <= r <= n$。可以证明，$S$ 中元素每次取 $r$ 个的组合数为：

$$
\frac{n!}{r!(n-r)!}
$$

请注意，$S$ 每次取 $r$ 个的组合数仅取决于 $r$ 和 $n$，而不取决于 $S$。这个数称为每次从 $n$ 个对象中取 $r$ 个的**组合**，或 **$n$ 选 $r$**，写作：

$$
{}_nC_r = \frac{n!}{r!(n-r)!}
$$

我们可以将实验的结果和事件的发生视为集合。由实验的所有结果组成的集合称为实验的**样本空间**，由表示事件发生的所有结果组成的集合称为**事件空间**。请注意，事件空间是样本空间的子集。回顾一下，集合是唯一元素的明确定义的集合，元素列出的顺序不重要。如果我们假设实验的所有结果都等可能发生，这通常是正确的但难以证明，那么：

$$
P(E) = \frac{\text{size of the event space}}{\text{size of the sample space}}
$$

我们现在计算从一副 52 张的牌中抽取 2 张 K 的概率。实验是从一副 52 张的牌中抽取 2 张卡片；因此，样本空间的大小是数字：

$$
{}_{52}C_2 = \frac{52!}{2!(52-2)!} = \frac{52(51)(50!)}{2!(50!)} = \frac{52(51)}{2} = 1326
$$

事件是从一副恰好包含 4 张 K 的牌中抽取 2 张 K；因此，事件空间的大小是数字：

$$
{}_4C_2 = \frac{4!}{2!(4-2)!} = \frac{4(3)(2!)}{2!(2!)} = \frac{4(3)}{2} = 6
$$

从一副 52 张的牌中抽取 2 张 K 的概率是 $\frac{6}{1326} = 0.00452489$。因为我们的事件空间大小为 6，我们列出集合中的元素以作说明。

```
event space =
{(King of Spades, King of Hearts), (King of Spades, King of Diamonds),
(King of Spades, King of Clubs), (King of Hearts, King of Diamonds),
(King of Hearts, King of Clubs), (King of Diamonds, King of Clubs)}
```

如前所述，我们可以使用计算机模拟来验证我们的分析结果。随着实验次数的增加，模拟概率应趋近于解析计算的概率。

开发一个程序，将事件的解析概率与模拟结果进行比较。对于此程序，事件是从一副 52 张的牌中抽取 2 张卡片，其中每张卡片都是红色的且每张卡片的面值都小于 10。允许用户输入模拟中使用的实验次数。

## 1. 问题描述

比较从一副洗好的 52 张牌中抽取 2 张卡片的解析概率和模拟概率，其中每张抽取的卡片都是红色的且面值小于 10。

## 2. 输入/输出描述

I/O 图显示，输入值是模拟中要进行的实验次数。输出是解析概率和模拟结果。

![](img/f2bfa570e453b020c16e048c79a3ea0e_380_0.png)

## 3. 手算示例

对于手算示例，我们将通过确定事件空间的大小，然后将该数字除以样本空间的大小来计算解析结果。在一副 52 张的牌中，有 8 张面值小于 10 的红桃和 8 张面值小于 10 的方块，总共 16 张面值小于 10 的红牌。因此，事件空间的大小是：

$$
{}_{16}C_2 = \frac{16!}{2!(16-2)!} = \frac{16(15)}{2!} = 120
$$

如前所述，样本空间为 1,326；因此，抽取 2 张红牌且每张面值都小于 10 的概率是 120/1326 = 0.09049774。

要手动进行该实验，我们需要：

- 洗牌。
- 从牌组中抽取 2 张卡片。
- 查看结果。
- 如果两张卡片都是红色的且两张卡片的面值都小于 10，则我们记录该事件，并将抽取的 2 张卡片放回牌组。

我们重复该实验 $n$ 次，然后将记录的事件数除以 $n$。如果你有一副牌，请进行 10 次该实验。你的结果是什么？即使进行 10 次该实验也很繁琐，我们必须小心保持准确的计数。因此，计算机模拟是可取的。

为了支持我们的模拟，我们将开发一个 Card 类和一个 CardDeck 类。我们的 Card 类需要两个属性：一个用于花色，一个用于面值或等级。当我们抽取一张 Card 时，我们需要“查看结果”，因此我们将包含两个访问器方法。我们还将包含一个方法，以以下格式显示一张卡片：

```
Ace of Spades if the rank is 14 and the suit is 'S', or
10 of Diamonds if the rank is 10 and the suit is 'D',
and so on.
```

我们的类中不包含修改器，因为卡片的概念是不可变的，意味着一旦创建，其值就不能更改。

我们的 CardDeck 类需要两个属性：一个向量用于存储牌组中的 52 张卡片，第二个向量用于保存我们从牌组中抽取的卡片。CardDeck 的功能需要一个洗牌方法和一个从 CardDeck 中抽取 Card 的方法。洗牌方法将负责替换从牌组中抽取的卡片，并将使用 <algorithm> 中定义的 random_shuffle() 方法来执行洗牌。

Card 和 CardDeck 的类图如图 7.6 所示。请注意连接两个类图的实心菱形连接器。该连接器表示类组合。我们说 CardDeck "has-a" Card。52 的标记指定 CardDeck 恰好有 52 个 Card 对象。类组合和 UML 类图将在第 10 章中更详细地讨论。类定义如下。

## 类定义：

### Card.h

```
/************************************************************** */
/* We use the following compiler directives to avoid */
/* including the Card.h file multiple times. */
/* */
/* It is a good idea to always use these directives */
/* in custom header files. */
/* */
#ifndef CARD_H
#define CARD_H
/* Card Class declaration */
/* filename: Card.h */
/* */
#include<iostream> //Required for ostream
using namespace std;

class Card {
public:
//Constructors
Card(); //Default
Card(char aSuit, int aRank);//parameterized
//Accessors
int getRank() const;
char getSuit() const;
//Formatted Display Method
//Example: if char is 'S' and rank is 11
//output will be:
//Jack of Spades
void displayCard(ostream& outStream) const;
private:
char suit;
int rank;
};
#endif //end compiler directive ifndef
/*-----------------------------------------------------*/
Card.cpp
/*-----------------------------------------------------*/
/* Card class implementation */
/* filename: Card.cpp */
/*-----------------------------------------------------*/
#include "Card.h" //Required for Card
#include <cctype> //Required for toupper()
#include <string> //Required for string
#include<iostream> //required for ostream
using namespace std;
//Constructors.
Card::Card():rank(2), suit('S')
{
}
Card::Card(char ch, int i): rank(i)
{
suit=toupper(ch);
}
//Accessor Methods
int Card::getRank() const
{
return rank;
}
char Card::getSuit() const
{
return suit;
}
```

