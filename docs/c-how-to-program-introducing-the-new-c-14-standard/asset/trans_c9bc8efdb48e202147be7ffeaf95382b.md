

| 运算符 | 结合性 | 描述 |
| --- | --- | --- |
| `()` `[]` `.` `->` `++` `--`<br>`static_cast<type>()` | 从左到右 | 后缀 |
| `++` `--` `+` `-` `!` `delete`<br>`sizeof`<br>`*` `~` `&` `new` | 从右到左 | 前缀 |
| `*` `/` `%` | 从左到右 | 乘法 |
| `+` `-` | 从左到右 | 加法 |
| `<<` `>>` | 从左到右 | 移位 |
| `<` `<=` `>` `>=` | 从左到右 | 关系 |
| `==` `!=` | 从左到右 | 相等性 |
| `&` | 从左到右 | 按位与 |
| `^` | 从左到右 | 按位异或 |
| `\|` | 从左到右 | 按位或 |
| `&&` | 从左到右 | 逻辑与 |
| `\|\|` | 从左到右 | 逻辑或 |
| `?:` | 从右到左 | 条件 |
| `=` `+=` `-=` `*=` `/=` `%=` `&=` `\|=`<br>`^=` `<<=` `>>=` | 从右到左 | 赋值 |
| `,` | 从左到右 | 逗号 |

## C++14 二进制字面量

从 C++14 开始，现在可以在源代码中包含`二进制字面量`。为此，请在一串 1 和 0 前加上`0b`或`0B`。例如，可以像本节示例中的`displayBits`函数那样，定义一个 32 位掩码：

```cpp
0b10000000'10000000'00000000'00000000
```

上述字面量还使用了 C++14 的单引号字符来分隔数字组，以提高可读性。

## 22.6 位域

C++ 提供了指定类或结构中整型或`enum`类型成员所占用位数的功能。这样的成员称为`位域`。位域通过使用存储数据所需的最少位数来实现*更好的内存利用率*。位域成员*必须声明*为整型或`enum`类型。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2564_0.png)

### 性能提示 22.1

*位域有助于节省存储空间。*

请考虑以下结构定义：

```cpp
struct BitCard {
    unsigned face : 4;
    unsigned suit : 2;
    unsigned color : 1;
};
```

该定义包含三个`unsigned`位域——`face`、`suit`和`color`——用于表示一副 52 张牌的牌组中的一张牌。声明位域时，应在整型或`enum`类型成员后面加上冒号（`:`）和一个表示`位域`宽度的整型常量（即存储该成员所需的位数）。宽度必须是整型常量。

前面的结构定义表示：成员`face`存储在 4 个位中，成员`suit`存储在 2 个位中，成员`color`存储在 1 个位中。位数取决于每个结构成员所需表示的值范围。成员`face`存储介于`0`（A）和`12`（K）之间的值——4 个位可以存储介于 0 和 15 之间的值。成员`suit`存储介于`0`和`3`之间的值（`0` = 方块，`1` = 红心，`2` = 梅花，`3` = 黑桃）——2 个位可以存储介于 0 和 3 之间的值。最后，成员`color`存储`0`（红色）或`1`（黑色）——1 个位可以存储 0 或 1。

[Figs. 22.14–22.16] 中的程序创建了一个包含`BitCard`结构的`array deck`（[Fig. 22.14] 的第 23 行）。构造函数将 52 张牌插入`deck array`，函数`deal`则输出这 52 张牌。注意，位域的访问方式与其他结构成员完全相同（[Fig. 22.15] 的第 12–14 行和第 22–27 行）。包含成员`color`是为了表示牌的颜色。

```cpp
// Fig. 22.14: DeckOfCards.h
// Definition of class DeckOfCards that
// represents a deck of playing cards.
#include <array>

// BitCard structure definition with bit fields
struct BitCard {
    unsigned face : 4; // 4 bits; 0-15
    unsigned suit : 2; // 2 bits; 0-3
    unsigned color : 1; // 1 bit; 0-1
};

// DeckOfCards class definition
class DeckOfCards {
public:
    static const int faces{13};
    static const int colors{2}; // black and red
    static const int numberOfCards{52};

    DeckOfCards(); // constructor initializes deck
    void deal() const; // deals cards in deck
private:
    std::array<BitCard, numberOfCards> deck; // represents deck of cards
};
```

图 22.14 表示一副扑克牌的`DeckOfCards`类的定义。

```cpp
// Fig. 22.15: DeckOfCards.cpp
// Member-function definitions for class DeckOfCards that simulates
// the shuffling and dealing of a deck of playing cards.
#include <iostream>
#include <iomanip>
#include "DeckOfCards.h" // DeckOfCards class definition
using namespace std;

// no-argument DeckOfCards constructor initializes deck
DeckOfCards::DeckOfCards() {
    for (size_t i{0}; i < deck.size(); ++i) {
        deck[i].face = i % faces; // faces in order
        deck[i].suit = i / faces; // suits in order
        deck[i].color = i / (faces * colors); // colors in order
    }
}

// deal cards in deck
void DeckOfCards::deal() const {
    for (size_t k1{0}, k2{k1 + deck.size() / 2};
         k1 < deck.size() / 2; ++k1, ++k2) {
        cout << "Card:" << setw(3) << deck[k1].face
             << " Suit:" << setw(2) << deck[k1].suit
             << " Color:" << setw(2) << deck[k1].color
             << "   " << "Card:" << setw(3) << deck[k2].face
             << " Suit:" << setw(2) << deck[k2].suit
             << " Color:" << setw(2) << deck[k2].color << endl;
    }
}
```

图 22.15 `DeckOfCards`类的成员函数定义。

```cpp
// Fig. 22.16: fig22_16.cpp
// Card shuffling and dealing program.
#include "DeckOfCards.h" // DeckOfCards class definition

int main() {
    DeckOfCards deckOfCards; // create DeckOfCards object
    deckOfCards.deal(); // deal the cards in the deck
}
```

```text
Card:  0  Suit: 0  Color: 0   Card:  0  Suit: 2  Color: 1
Card:  1  Suit: 0  Color: 0   Card:  1  Suit: 2  Color: 1
Card:  2  Suit: 0  Color: 0   Card:  2  Suit: 2  Color: 1
Card:  3  Suit: 0  Color: 0   Card:  3  Suit: 2  Color: 1
Card:  4  Suit: 0  Color: 0   Card:  4  Suit: 2  Color: 1
Card:  5  Suit: 0  Color: 0   Card:  5  Suit: 2  Color: 1
Card:  6  Suit: 0  Color: 0   Card:  6  Suit: 2  Color: 1
Card:  7  Suit: 0  Color: 0   Card:  7  Suit: 2  Color: 1
Card:  8  Suit: 0  Color: 0   Card:  8  Suit: 2  Color: 1
Card:  9  Suit: 0  Color: 0   Card:  9  Suit: 2  Color: 1
Card: 10  Suit: 0  Color: 0   Card: 10  Suit: 2  Color: 1
Card: 11  Suit: 0  Color: 0   Card: 11  Suit: 2  Color: 1
Card: 12  Suit: 0  Color: 0   Card: 12  Suit: 2  Color: 1
Card:  0  Suit: 1  Color: 0   Card:  0  Suit: 3  Color: 1
Card:  1  Suit: 1  Color: 0   Card:  1  Suit: 3  Color: 1
Card:  2  Suit: 1  Color: 0   Card:  2  Suit: 3  Color: 1
Card:  3  Suit: 1  Color: 0   Card:  3  Suit: 3  Color: 1
Card:  4  Suit: 1  Color: 0   Card:  4  Suit: 3  Color: 1
Card:  5  Suit: 1  Color: 0   Card:  5  Suit: 3  Color: 1
Card:  6  Suit: 1  Color: 0   Card:  6  Suit: 3  Color: 1
Card:  7  Suit: 1  Color: 0   Card:  7  Suit: 3  Color: 1
Card:  8  Suit: 1  Color: 0   Card:  8  Suit: 3  Color: 1
Card:  9  Suit: 1  Color: 0   Card:  9  Suit: 3  Color: 1
Card: 10  Suit: 1  Color: 0   Card: 10  Suit: 3  Color: 1
Card: 11  Suit: 1  Color: 0   Card: 11  Suit: 3  Color: 1
Card: 12  Suit: 1  Color: 0   Card: 12  Suit: 3  Color: 1
```

图 22.16 用于存储一副牌的位域。

还可以指定一个`未命名位域`，此时该字段在结构中用作`填充`。例如，下面的结构定义使用一个未命名的三位字段作为填充——这三个位中不能存储任何内容。成员`b`存储在另一个存储单元中。

```c
struct Example {
    unsigned a : 13;
    unsigned   : 3; // align to next storage-unit boundary
    unsigned b : 4;
};
```

**宽度为 0 的未命名位域**用于将下一个位域对齐到新的存储单元边界。例如，结构定义：

```c
struct Example {
    unsigned a : 13;
    unsigned   : 0; // align to next storage-unit boundary
    unsigned b : 4;
};
```

使用未命名的**0**位字段来*跳过*存储成员**a**的存储单元中剩余的位（无论有多少），并将**b**对齐到*下一个存储单元边界*。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2569_0.png)

### 可移植性提示 22.4

