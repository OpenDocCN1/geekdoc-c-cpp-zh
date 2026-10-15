The definition contains three unsigned bit fields—face, suit and color—used to represent a card from a deck of 52 cards. A bit field is declared by following an integral type or enum type member with a colon (:) and an integer constant representing the *width of the bit field* (i.e., the number of bits in which the member is stored). The width must be an integer constant.

The preceding structure definition indicates that member face is stored in 4 bits, member suit in 2 bits and member color in 1 bit. The number of bits is based on the desired range of values for each structure member. Member face stores values between 0 (Ace) and 12 (King)—4 bits can store a value between 0 and 15. Member suit stores values between 0 and 3 (0 = Diamonds, 1 = Hearts, 2 = Clubs, 3 = Spades)—2 bits can store a value between 0 and 3. Finally, member color stores either 0 (Red) or 1 (Black)—1 bit can store either 0 or 1.

The program in Figs. 19.14–19.16 creates array deck containing 52 BitCard structures (line 21 of Fig. 19.14). The constructor inserts the 52 cards in the deck array, and function deal prints the 52 cards. Notice that bit fields are accessed exactly as any other structure member is (lines 18–20 and 28–33 of Fig. 19.15). The member color is included as a means of indicating the card color on a system that allows color displays.

```
```cpp
// Fig. 19.14: DeckOfCards.h
// Definition of class DeckOfCards that
// represents a deck of playing cards.

// BitCard structure definition with bit fields
struct BitCard
{
   unsigned face : 4; // 4 bits; 0-15
   unsigned suit : 2; // 2 bits; 0-3
   unsigned color : 1; // 1 bit; 0-1
}; // end struct BitCard

// DeckOfCards class definition
class DeckOfCards
{
public:
   DeckOfCards(); // constructor initializes deck
   void deal(); // deals cards in deck

private:
   BitCard deck[ 52 ]; // represents deck of cards
}; // end class DeckOfCards
```
```

**Fig. 19.14** | Header file for class DeckOfCards.

```
```cpp
// Fig. 19.15: DeckOfCards.cpp
// Member-function definitions for class DeckOfCards that simulates
// the shuffling and dealing of a deck of playing cards.
#include <iostream>
using std::cout;
```
```

**Fig. 19.15** | Class file for DeckOfCards. (Part 1 of 2.)