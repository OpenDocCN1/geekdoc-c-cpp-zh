
```c
struct Example {
    char c;
    int i;
} sample1, sample2;
```

A computer with two-byte words might require that each of the members of `Example` be aligned on a word boundary (i.e., at the beginning of a word—this is *machine dependent*). **Figure 22.1** shows a sample storage alignment for an object of type `Example` that’s been assigned the character `'a'` and the integer `97` (the bit representations of the values are shown). If the members are stored beginning at word boundaries, there is a one-byte hole (byte `1` in the figure) in the storage for objects of type `Example`. The value in the one-byte hole is *undefined*. If the values in `sample1` and `sample2` are in fact equal, the structure objects might *not* be equal, because the *undefined* one-byte holes are not likely to contain identical values.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2538_0.png)

### Portability Tip 22.1

*Because the size of data items of a particular type is machine dependent, and because storage alignment considerations are machine dependent, so too is the representation of a structure.*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2539_0.png)

### Common Programming Error 22.1

*Comparing variables of structure types is a compilation error.*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2539_1.png)

**Fig. 22.1** Possible storage alignment for an `Example` object, showing an undefined byte.

## 22.3 `typedef` and `using`

Keyword `typedef` provides a mechanism for creating *synonyms* (or *aliases*) for previously defined data types. Names for structure types are often defined with `typedef` to more readable type names. For example, the statement

```cpp
typedef Card* CardPtr;
```

defines the new type name `CardPtr` as a synonym for type `Card*`. Creating a new name with `typedef` does *not* create a new type; `typedef` simply creates a *new type name* that can then be used in the program as an alias for an existing type name.

C++11 added the keyword `using` as another mechanism for creating type aliases. The following declaration is equivalent to the `typedef` above:

```cpp
using CardPtr = Card*;
```

This feature was added to fix problems with `typedef` in template programming.

## 22.4 Example: Card Shuffling and Dealing Simulation

The card shuffling and dealing program in **Figs. 22.2–22.4** is similar to the one described in **Exercise 9.23**. This program represents the deck of cards as an `array` of structures.

```cpp
// Fig. 22.2: DeckOfCards.h
// Definition of class DeckOfCards that
// represents a deck of playing cards.
#include <string>
#include <array>

// Card structure definition
struct Card {
   std::string face;
   std::string suit;
};

// DeckOfCards class definition
class DeckOfCards {
public:
   static const int numberOfCards{52};
   static const int faces{13};
   static const int suits{4};

   DeckOfCards(); // constructor initializes deck
   void shuffle(); // shuffles cards in deck
   void deal() const; // deals cards in deck

private:
   std::array<Card, numberOfCards> deck; // represents deck of cards
};
```

**Fig. 22.2** Definition of class `DeckOfCards` that represents a deck of playing cards.

The constructor (lines 12–27 of **Fig. 22.3**) initializes the `array` in order with character strings representing Ace through King of each suit. Function `shuffle` implements the shuffling algorithm. The function loops through all 52 cards (subscripts 0 to 51). For each card, a number between 0 and 51 is picked randomly. Next, the current `card` and the randomly selected `card` are swapped in the `array`. A total of 52 swaps are made in a single pass of the entire `array`, and the `array` is shuffled. Because the `Card` structures were swapped in place in the `array`, the dealing algorithm implemented in function `deal` requires only one pass of the `array` to deal the shuffled cards.

```cpp
// Fig. 22-3: DeckOfCards.cpp
// Member-function definitions for class DeckOfCards that simulates
// the shuffling and dealing of a deck of playing cards.
#include <iostream>
#include <iomanip>
#include <cstdlib> // prototypes for rand and srand
#include <ctime> // prototype for time
#include "DeckOfCards.h" // DeckOfCards class definition
using namespace std;

// no-argument DeckOfCards constructor initializes deck
DeckOfCards::DeckOfCards() {
   // initialize suit array
   static string suit[suits]{"Hearts", "Diamonds", "Clubs", "Spades"};

   // initialize face array
   static string face[faces]{"Ace", "Deuce", "Three", "Four", "Five",
      "Six", "Seven", "Eight", "Nine", "Ten", "Jack", "Queen", "King"};

   // set values for deck of 52 Cards
   for (size_t i{0}; i < deck.size(); ++i) {
      deck[i].face = face[i % faces];
      deck[i].suit = suit[i % faces];
   }

   srand(static_cast< size_t >(time(nullptr))); // seed
}

// shuffle cards in deck
void DeckOfCards::shuffle() {
   // shuffle cards randomly
   for (size_t i{0}; i < deck.size(); ++i) {
      int j{rand() % numberOfCards};
      Card temp = deck[i];
      deck[i] = deck[j];
      deck[j] = temp;
   }
}

// deal cards in deck
void DeckOfCards::deal() const {
   // display each card’s face and suit
   for (size_t i = 0; i < deck.size(); ++i) {
      cout << right << setw(5) << deck[i].face << " of "
         << left << setw(8) << deck[i].suit
         << ((i + 1) % 2 ? '\t' : '\n');
   }
}
```

**Fig. 22.3** Member-function definitions for class `DeckOfCards`.

```cpp
// Fig. 22.4: fig22_04.cpp
// Card shuffling and dealing program.
#include "DeckOfCards.h" // DeckOfCards class definition

int main() {
    DeckOfCards deckOfCards; // create DeckOfCards object
    deckOfCards.shuffle();   // shuffle the cards in the deck
    deckOfCards.deal();      // deal the cards in the deck
}
```

```text
King of Clubs          Ten of Diamonds
Five of Diamonds       Jack of Clubs
Seven of Spades        Five of Clubs
Three of Spades        King of Hearts
Ten of Clubs           Eight of Spades
Eight of Hearts        Six of Hearts
Nine of Diamonds       Nine of Clubs
Three of Diamonds      Queen of Hearts
Six of Clubs           Seven of Hearts
Seven of Diamonds      Jack of Diamonds
Jack of Spades         King of Diamonds
Deuce of Diamonds      Four of Clubs
Three of Clubs         Five of Hearts
Eight of Clubs         Ace of Hearts
Deuce of Spades        Ace of Clubs
Ten of Spades          Eight of Diamonds
Ten of Hearts          Six of Spades
Queen of Diamonds      Nine of Hearts
Seven of Clubs         Queen of Clubs
Deuce of Clubs         Queen of Spades
Three of Hearts        Five of Spades
Deuce of Hearts        Jack of Hearts
Four of Hearts         Ace of Diamonds
Nine of Spades         Four of Diamonds
Ace of Spades          Six of Diamonds
Four of Spades         King of Spades
```

**Fig. 22.4** Card shuffling and dealing program.

## 22.5 Bitwise Operators

C++ provides extensive *bit-manipulation* capabilities for getting down to the so-called “bits-and-bytes” level. Operating systems, test-equipment software, networking software and many other kinds of software require that you communicate “directly with the hardware.” We introduce each of the *bitwise operators*, and we discuss how to save memory by using *bit fields*.

All data is represented internally by computers as sequences of bits. Each bit can assume the value `0` or the value `1`. On most systems, a sequence of eight bits, each of which forms a byte—the standard storage unit for a variable of type `char`. Other data types are stored in larger numbers of bytes. Bitwise operators are used to manipulate the bits of integral operands (`char`, `short`, `int` and `long`; both `signed` and `unsigned`). Normally the bitwise operators are used with unsigned integers.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2546_0.png)

### Portability Tip 22.2

> *Bitwise data manipulations are machine dependent.*
