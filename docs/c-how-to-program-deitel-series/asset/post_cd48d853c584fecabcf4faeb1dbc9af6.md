
## 22 Bits, Characters, C Strings and **structs**

![](img/b42ba5cd262b1358d16610173f975e4d_914_0.png)

> The same old charitable lie
> Repeated as the years scoot by
> Perpetually makes a bit—
> “You really haven't changed a bit!”
>
> —Margaret Fishback

> The chief defect of Henry King
> Was chewing little bits of string.
>
> —Hilaire Belloc

> Vigorous writing is concise. A
> sentence should contain no
> unnecessary words, a paragraph
> no unnecessary sentences.
>
> —William Strunk, Jr.

### Objectives

In this chapter you'll learn:

- To create and use structs and to understand their near equivalence with classes.
- To use typedef to create aliases for data types.
- To manipulate data with the bitwise operators and to create bit fields for storing data compactly.
- To use the functions of the character-handling library `<cctype>`.
- To use the string-conversion functions of the general-utilities library `<cstdlib>`.
- To use the string-processing functions of the string-handling library `<cstring>`.

![](img/b42ba5cd262b1358d16610173f975e4d_915_0.png)

| Section | Title | Section | Title |
|---|---|---|---|
| 22.1 | Introduction | 22.8 | C String-Manipulation Functions |
| 22.2 | Structure Definitions | 22.9 | C String-Conversion Functions |
| 22.3 | typedef | 22.10 | Search Functions of the C String-Handling Library |
| 22.4 | Example: Card Shuffling and Dealing Simulation | 22.11 | Memory Functions of the C String-Handling Library |
| 22.5 | Bitwise Operators | 22.12 | Wrap-Up |
| 22.6 | Bit Fields |  |  |
| 22.7 | Character-Handling Library |  |  |

| Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises | Special Section: Advanced String-Manipulation Exercises | Challenging String-Manipulation Projects |
|---|---|---|---|---|---|

### 22.1 Introduction

We now discuss structures, their near equivalence with classes, and the manipulation of bits, characters and C strings. Many of the techniques we present here are included for the benefit of those who will work with legacy C and C++ code.

Like classes, C++ structures may contain access specifiers, member functions, constructors and destructors. In fact, the only differences between structures and classes in C++ is that structure members default to public access and class members default to private access when no access specifiers are used, and that structures default to public inheritance, whereas classes default to private inheritance. Our presentation of structures here is typical of the legacy C code and early C++ code you’ll see in industry.

We present a high-performance card shuffling and dealing simulation in which we use structure objects containing C++ string objects to represent the cards. We discuss the bitwise operators that allow you to access and manipulate the individual bits in bytes of data. We also present bitfields—special structures that can be used to specify the exact number of bits a variable occupies in memory. These bit-manipulation techniques are common in programs that interact directly with hardware devices that have limited memory. The chapter finishes with examples of many character and C string-manipulation functions—some of which are designed to process blocks of memory as arrays of bytes. The detailed C string treatment in this chapter is mostly for reasons of legacy code support and because there are still remnants of C string use in C++, such as command-line arguments (Appendix F). New development should use C++ string objects rather than C strings.

### 22.2 Structure Definitions

Consider the following structure definition:

```cpp
struct Card
{
    string face;
    string suit;
}; // end struct Card
```

Keyword struct introduces the definition for structure Card. The identifier Card is the structure name and is used in C++ to declare variables of the structure type (in C, the type is struct Card).

![](img/b42ba5cd262b1358d16610173f975e4d_917_0.png)

**Fig. 22.1** | Possible storage alignment for an *Example* object, showing an undefined byte.

### 22.3 typedef

Keyword **typedef** provides a mechanism for creating *synonyms* (or *aliases*) for previously defined data types. Names for structure types are often defined with typedef to more readable type names. For example, the statement

```cpp
typedef Card *CardPtr;
```

defines the new type name `CardPtr` as a synonym for type `Card *`.

Creating a new name with typedef does not create a new type; typedef simply creates a *new type name* that can then be used in the program as an alias for an existing type name.

### 22.4 Example: Card Shuffling and Dealing Simulation

The card shuffling and dealing program in Figs. 22.2–22.4 is similar to the one described in Exercise 9.23. This program represents the deck of cards as an array of structures.

```cpp
// Fig. 22.2: DeckOfCards.h
// Definition of class DeckOfCards that
// represents a deck of playing cards.
#include <string>
#include <array>

// Card structure definition
struct Card
{
   std::string face;
   std::string suit;
}; // end structure Card

// DeckOfCards class definition
class DeckOfCards
{
public:
   static const int numberOfCards = 52;
   static const int faces = 13;
   static const int suits = 4;

   DeckOfCards(); // constructor initializes deck
   void shuffle(); // shuffles cards in deck
   void deal(); // deals cards in deck
```

**Fig. 22.2** | Definition of class `DeckOfCards` that represents a deck of playing cards. (Part 1 of 2.)

```cpp
// shuffle cards randomly
for ( size_t i = 0; i < deck.size(); ++i )
{
   int j = rand() % numberOfCards;
   Card temp = deck[ i ];
   deck[ i ] = deck[ j ];
   deck[ j ] = temp;
} // end function shuffle

// deal cards in deck
void DeckOfCards::deal() const
{
   // display each card's face and suit
   for ( size_t i = 0; i < deck.size(); ++i )
      cout << right << setw( 5 ) << deck[ i ].face << " of "
           << left << setw( 8 ) << deck[ i ].suit
           << ( ( i + 1 ) % 2 ? '\t' : '\n' );
} // end function deal
```

**Fig. 22.3** | Member-function definitions for class DeckOfCards. (Part 2 of 2.)

```cpp
// Fig. 22.4: fig22_04.cpp
// Card shuffling and dealing program.
#include "DeckOfCards.h" // DeckOfCards class definition

int main()
{
   DeckOfCards deckOfCards; // create DeckOfCards object
   deckOfCards.shuffle(); // shuffle the cards in the deck
   deckOfCards.deal(); // deal the cards in the deck
} // end main
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
```

**Fig. 22.4** | Card shuffling and dealing program. (Part 1 of 2.)

### 22.5 Bitwise Operators

| Operator | Name | Description |
|---|---|---|
| `&` | bitwise AND | The bits in the result are set to 1 if the corresponding bits in the two operands are both 1. |
| `\|` | bitwise inclusive OR | The bits in the result are set to 1 if one or both of the corresponding bits in the two operands is 1. |
| `^` | bitwise exclusive OR | The bits in the result are set to 1 if exactly one of the corresponding bits in the two operands is 1. |
| `<<` | left shift | Shifts the bits of the first operand left by the number of bits specified by the second operand; fill from right with 0 bits. |
| `>>` | right shift with sign extension | Shifts the bits of the first operand right by the number of bits specified by the second operand; the method of filling from the left is machine dependent. |
| `~` | bitwise complement | All 0 bits are set to 1 and all 1 bits are set to 0. |

**Fig. 22.5** | Bitwise operators.

#### Printing a Binary Representation of an Integral Value

When using the bitwise operators, it’s useful to illustrate their precise effects by printing values in their binary representation. The program of Fig. 22.6 prints an unsigned integer in its binary representation in groups of eight bits each.

```cpp
// Fig. 22.6: Fig22_06.cpp
// Printing an unsigned integer in bits.
#include <iostream>
#include <iomanip>
using namespace std;

void displayBits( unsigned ); // prototype

int main()
{
    unsigned inputValue = 0; // integral value to print in binary

    cout << "Enter an unsigned integer: ";
    cin >> inputValue;
    displayBits( inputValue );
} // end main

// display bits of an unsigned integer value
void displayBits( unsigned value )
{
    const int SHIFT = 8 * sizeof( unsigned ) - 1;
    const unsigned MASK = 1 << SHIFT;

    cout << setw( 10 ) << value << " = ";
}
```

**Fig. 22.6** | Printing an unsigned integer in bits. (Part 1 of 2.)
