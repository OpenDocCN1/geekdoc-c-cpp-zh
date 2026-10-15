

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_363_0.png)

## Fig. 8.23 | 牌堆的二维数组表示。

该模拟牌堆可按如下方式洗牌。首先，52 个元素的数组 deck 初始化为零。然后，随机各选择一行 0–3 和一列 0–12。数字 1 插入到数组元素 `deck[row][column]` 中，表示该牌将成为洗好后发出的第一张牌。此过程继续进行，数字 2、3、…、52 被随机插入到 deck 数组中，以表示哪些牌应放在洗好牌堆中的第二张、第三张、…、第 52 张位置。随着 deck 数组开始填入牌号，可能会出现一张牌被重复选中，即 `deck[row][column]` 在被选中时不为零。这种选择 simply 被忽略，并反复随机选择其他行列组合，直到找到一张未被选中的牌。最终，数字 1 到 52 将占据 deck 数组的 52 个槽位。此时，牌堆已完全洗好。

如果反复随机选择已经洗过的牌，该洗牌算法可能会无限期地执行下去。这种现象被称为 **无限期推迟**，也称为 **饥饿**。

## Performance Tip 8.3

> 有时以“自然”方式出现的算法可能包含诸如无限期推迟之类的微妙性能问题。请寻找避免无限期推迟的算法。

要发第一张牌，我们在数组中搜索与 1 匹配的元素 `deck[row][column]`。这是通过嵌套的 for 语句实现的，该语句使 row 从 0 变到 3，column 从 0 变到 12。数组的该槽位对应于哪张牌？suit 数组已预先加载了四种花色，因此要获取花色，我们打印字符字符串 `suit[row]`。同样，要获取牌的点数，我们打印字符字符串 `face[column]`。我们还打印字符字符串 " of "。以正确的顺序打印这些信息使我们能够以 "King of Clubs"、"Ace of Diamonds" 等形式打印每张牌。

图 8.24–8.26 包含洗牌和发牌程序以及一个示例执行。注意图 8.25 中函数 `deal` 的输出格式，第 81–83 行。输出语句将 face 右对齐输出到宽度为 5 个字符的字段中，并将 suit 左对齐输出到宽度为 8 个字符的字段中（图 8.26）。输出以两列格式打印——如果输出的牌在第一列，则在牌后输出一个制表符以移动到第二列（第 83 行）；否则，输出一个换行符。

```
// Fig. 8.24: DeckOfCards.h
// Definition of class DeckOfCards that
// represents a deck of playing cards.

// DeckOfCards class definition
class DeckOfCards
{
public:
    DeckOfCards(); // constructor initializes deck
    void shuffle(); // shuffles cards in deck
    void deal(); // deals cards in deck
private:
    int deck[ 4 ][ 13 ]; // represents deck of cards
}; // end class DeckOfCards
```

Fig. 8.24 | DeckOfCards 头文件。

```
// Fig. 8.25: DeckOfCards.cpp
// Member-function definitions for class DeckOfCards that simulates
// the shuffling and dealing of a deck of playing cards.
#include <iostream>
using std::cout;
using std::left;
using std::right;

#include <iomanip>
using std::setw;

#include <cstdlib> // prototypes for rand and srand
using std::rand;
using std::srand;

#include <ctime> // prototype for time
using std::time;

#include "DeckOfCards.h" // DeckOfCards class definition

// DeckOfCards default constructor initializes deck
DeckOfCards::DeckOfCards()
{
    // loop through rows of deck
    for ( int row = 0; row <= 3; row++ )
    {
        // loop through columns of deck for current row
        for ( int column = 0; column <= 12; column++ )
        {
            deck[ row ][ column ] = 0; // initialize slot of deck to 0
        } // end inner for
    } // end outer for

    srand( time( 0 ) ); // seed random number generator
} // end DeckOfCards default constructor
```

Fig. 8.25 | 洗牌和发牌成员函数的定义。 第 1 部分，共 2 部分。

```
```cpp
// shuffle cards in deck
void DeckOfCards::shuffle()
{
    int row; // represents suit value of card
    int column; // represents face value of card

    // for each of the 52 cards, choose a slot of the deck randomly
    for ( int card = 1; card <= 52; card++ )
    {
        do // choose a new random location until unoccupied slot is found
        {
            row = rand() % 4; // randomly select the row (0 to 3)
            column = rand() % 13; // randomly select the column (0 to 12)
        } while( deck[ row ][ column ] != 0 ); // end do...while

        // place card number in chosen slot of deck
        deck[ row ][ column ] = card;
    } // end for
} // end function shuffle

// deal cards in deck
void DeckOfCards::deal()
{
    // initialize suit array
    static const char *suit[ 4 ] =
        { "Hearts", "Diamonds", "Clubs", "Spades" };

    // initialize face array
    static const char *face[ 13 ] =
        { "Ace", "Deuce", "Three", "Four", "Five", "Six", "Seven",
          "Eight", "Nine", "Ten", "Jack", "Queen", "King" };

    // for each of the 52 cards
    for ( int card = 1; card <= 52; card++ )
    {
        // loop through rows of deck
        for ( int row = 0; row <= 3; row++ )
        {
            // loop through columns of deck for current row
            for ( int column = 0; column <= 12; column++ )
            {
                // if slot contains current card, display card
                if ( deck[ row ][ column ] == card )
                {
                    cout << setw( 5 ) << right << face[ column ]
                         << " of " << setw( 8 ) << left << suit[ row ]
                         << ( card % 2 == 0 ? '\n' : '\t' );
                } // end if
            } // end innermost for
        } // end inner for
    } // end outer for
} // end function deal
```
```

**Fig. 8.25** | 洗牌和发牌成员函数的定义。 第 2 部分，共 2 部分。

```
// Fig. 8.26: fig08_26.cpp
// Card shuffling and dealing program.
#include "DeckOfCards.h" // DeckOfCards class definition

int main()
{
    DeckOfCards deckOfCards; // create DeckOfCards object

    deckOfCards.shuffle(); // shuffle the cards in the deck
    deckOfCards.deal(); // deal the cards in the deck
    return 0; // indicates successful termination
} // end main
```

Nine of Spades    Seven of Clubs
Five of Spades    Eight of Clubs
Queen of Diamonds Three of Hearts
Jack of Spades    Five of Diamonds
Jack of Diamonds  Three of Diamonds
Three of Clubs    Six of Clubs
Ten of Clubs      Nine of Diamonds
Ace of Hearts     Queen of Hearts
Seven of Spades   Deuce of Spades
Six of Hearts     Deuce of Clubs
Ace of Clubs      Deuce of Diamonds
Nine of Hearts    Seven of Diamonds
Six of Spades     Eight of Diamonds
Ten of Spades     King of Hearts
Four of Clubs     Ace of Spades
Ten of Hearts     Four of Spades
Eight of Hearts   Eight of Spades
Jack of Hearts    Ten of Diamonds
Four of Diamonds  King of Diamonds
Seven of Hearts   King of Spades
Queen of Spades   Four of Hearts
Nine of Clubs     Six of Diamonds
Deuce of Hearts   Jack of Clubs
King of Clubs     Three of Spades
Queen of Clubs    Five of Clubs
Five of Hearts    Ace of Diamonds

Fig. 8.26 | 牌洗牌和发牌程序。

发牌算法存在一个弱点。一旦找到匹配，即使在第一次尝试时找到，两个内部 for 语句仍会继续搜索 deck 的剩余元素以寻找匹配。

## 8.12 Function Pointers

函数指针包含内存中函数的地址。在第 7 章中，我们看到数组的名称实际上是数组第一个元素在内存中的地址。同样，函数的名称实际上是执行函数任务的代码在内存中的起始地址。函数指针可以传递给函数、从函数返回、存储在数组中、分配给其他函数指针并用于调用底层函数。

