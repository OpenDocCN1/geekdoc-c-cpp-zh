
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

**Fig. 8.25** | 洗牌和发牌成员函数的定义。 第 2 部分，共 2 部分。

```cpp
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

发牌算法存在一个弱点。一旦找到匹配，即使在第一次尝试时找到，两个内部 `for` 语句仍会继续搜索 `deck` 的剩余元素以寻找匹配。

# 8.12 Function Pointers

函数指针包含内存中函数的地址。在第 7 章中，我们看到数组的名称实际上是数组第一个元素在内存中的地址。同样，函数的名称实际上是执行函数任务的代码在内存中的起始地址。函数指针可以传递给函数、从函数返回、存储在数组中、分配给其他函数指针并用于调用底层函数。

## 使用函数指针的多用途选择排序

为了说明指向函数的指针的用法，图 8.27 修改了图 8.15 中的选择排序程序。图 8.27 由 `main`（第 17–55 行）以及函数 `selectionSort`（第 59–76 行）、`swap`（第 80–85 行）、`ascending`（第 89–92 行）和 `descending`（第 96–99 行）组成。函数 `selectionSort` 除了接收要排序的整数数组和数组大小作为参数外，还接收一个指向函数的指针——可以是函数 `ascending` 或函数 `descending`——作为参数。函数 `ascending` 和 `descending` 决定排序顺序。程序提示用户选择数组应按升序还是降序排序（第 24–26 行）。如果用户输入 1，则将指向函数 `ascending` 的指针传递给函数 `selectionSort`（第 37 行），使数组按升序排序。如果用户输入 2，则将指向函数 `descending` 的指针传递给函数 `selectionSort`（第 45 行），使数组按降序排序。

```cpp
// Fig. 8.27: fig08_27.cpp

// Multipurpose sorting program using function pointers.

#include <iostream>

using std::cout;

using std::cin;

using std::endl;

#include <iomanip>

using std::setw;

// prototypes

void selectionSort( int [], const int, bool (*)( int, int ) );

void swap( int * const, int * const );

bool ascending( int, int ); // implements ascending order

bool descending( int, int ); // implements descending order

int main()

{

    const int arraySize = 10;

    int order; // 1 = ascending, 2 = descending

    int counter; // array index

    int a[ arraySize ] = { 2, 6, 4, 8, 10, 12, 89, 68, 45, 37 };

    cout << "Enter 1 to sort in ascending order,\n"

         << "Enter 2 to sort in descending order: ";

    cin >> order;

    cout << "\nData items in original order\n";

    // output original array

    for ( counter = 0; counter < arraySize; counter++ )

        cout << setw( 4 ) << a[ counter ];

    // sort array in ascending order; pass function ascending

    // as an argument to specify ascending sorting order

    if ( order == 1 )

    {

        selectionSort( a, arraySize, ascending );

        cout << "\nData items in ascending order\n";

    } // end if

    // sort array in descending order; pass function descending

    // as an argument to specify descending sorting order

    else

    {

        selectionSort( a, arraySize, descending );

        cout << "\nData items in descending order\n";

    } // end else part of if...else

    // output sorted array

    for ( counter = 0; counter < arraySize; counter++ )

        cout << setw( 4 ) << a[ counter ];

    cout << endl;

    return 0; // indicates successful termination

} // end main

// multipurpose selection sort; the parameter compare is a pointer to

// the comparison function that determines the sorting order

void selectionSort( int work[], const int size,

                    bool (*compare)( int, int ) )

{

    int smallestOrLargest; // index of smallest (or largest) element

    // loop over size - 1 elements

    for ( int i = 0; i < size - 1; i++ )

    {

        smallestOrLargest = i; // first index of remaining vector

        // loop to find index of smallest (or largest) element

        for ( int index = i + 1; index < size; index++ )

            if ( !(*compare)( work[ smallestOrLargest ], work[ index ] ) )

                smallestOrLargest = index;

        swap( &work[ smallestOrLargest ], &work[ i ] );

    } // end if

} // end function selectionSort

// swap values at memory locations to which

// element1Ptr and element2Ptr point

void swap( int * const element1Ptr, int * const element2Ptr )

{

    int hold = *element1Ptr;

    *element1Ptr = *element2Ptr;

    *element2Ptr = hold;

} // end function swap

// determine whether element a is less than

// element b for an ascending order sort

bool ascending( int a, int b )

{

    return a < b; // returns true if a is less than b

} // end function ascending

// determine whether element a is greater than

// element b for a descending order sort

bool descending( int a, int b )

{

    return a > b; // returns true if a is greater than b

} // end function descending
```
