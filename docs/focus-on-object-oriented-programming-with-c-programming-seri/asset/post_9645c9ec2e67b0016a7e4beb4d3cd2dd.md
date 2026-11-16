
```cpp
// card.h
#ifndef CARD_H
#define CARD_H
class Card {
public:
// Define types for the suit and value
enum Suit { Diamonds, Hearts, Clubs, Spades };
enum Value { NullCard, Ace, Two, Three, Four, Five, Six,
Seven, Eight, Nine, Ten, Jack, Queen, King };
private:
static const char *names[4];
static const char *vnames[14];
Suit s;
Value v;
public:
// Constructors initialize a card
Card();
Card(Suit newSuit, Value newValue);
Suit getSuit(); // Returns a card's suit.
Value getValue(); // Returns a card's value.
void printSuit(); // Print a card's suit.
void printValue(); // Print a card's value.
void printCard(); // Print a card's suit and value.
};
// Return the next suit or card value in succession
Card::Suit nextSuit(Card::Suit);
Card::Value nextValue(Card::Value);
#endif
```

```cpp
// card.cpp
#include <iostream>
#include "card.h"
using namespace std;
const char * Card::names[4] = {"Diamonds", "Hearts", "Clubs",
                               "Spades" };
const char * Card::vnames[14] = {"Bad Card", "Ace", "2", "3", "4", "5",
                                 "6", "7", "8", "9", "10", "Jack",
                                 "Queen", "King" };
Card::Card() {
    v = NullCard;
}
Card::Card(Suit newSuit, Value newValue) {
    s = newSuit;
    v = newValue;
}
Card::Suit Card::getSuit() {
    return s;
}
Card::Value Card::getValue() {
    return v;
}
void Card::printSuit() {
    cout << names[s];
}
void Card::printValue() {
    cout << vnames[v];
}
void Card::printCard() {
    printValue();
    cout << " of ";
    printSuit();
}
Card::Suit nextSuit(Card::Suit s) {
    return(s+1 > Card::Spades ? Card::Diamonds : (Card::Suit) (s+1));
}
Card::Value nextValue(Card::Value v) {
    return(v+1 > Card::King ? Card::Ace : (Card::Value) (v+1));
}
```

```cpp
// deck.h

#ifndef _DECK_H
#define _DECK_H

#include "card.h"

const int DECKSIZE = 52;

class Deck {
    private:
        Card inDeck[DECKSIZE]; // These are private data members and
        int nextCard;          // can be used only by member functions.
    public:
        Deck();                // Initialization. Called automatically
                               // when a Deck variable is declared.
        void shuffle(int);     // Exchange random pairs of cards.
        Card getCard();        // Returns top card from the deck.
        void addCard(Card);    // Put named card in the deck.
        int totalCards();      // Returns number of cards left in deck.
};

#endif
```

```cpp
// deck.cpp

#include <stdlib.h>
#include "deck.h"

Deck::Deck() {
    int i;
    Card::Suit curSuit;
    Card::Value curValue;

    nextCard = 0;
    for(i = 0, curSuit = Card::Diamonds, curValue = Card::Ace;
        i < DECKSIZE; i++) {
        inDeck[i] = Card(curSuit, curValue);
        curValue = nextValue(curValue);
        if(curValue == Card::Ace)
            curSuit = nextSuit(curSuit);
    }
}

void Deck::shuffle(int swaps) {
    Card temp;

    for (int i = 0; i < swaps; i++) {
        int il = rand() % DECKSIZE;
        int i2 = rand() % DECKSIZE;
        temp = inDeck[il];
        inDeck[il] = inDeck[i2];
        inDeck[i2] = temp;
    }
}

Card Deck::getCard() {
    return(nextCard < DECKSIZE ? inDeck[nextCard++] :
        Card(Card::Clubs, Card::NullCard));
}

void Deck::addCard(Card newCard) {
    if(nextCard > 0)
        inDeck[--nextCard] = newCard;
}

int Deck::totalCards() {
    return DECKSIZE - nextCard;
}
```

## Chapter 5. Constructors and Destructors

- Introduction to Constructors and Destructors
- Arrays of Class Objects
- Constructor and Destructor Homework
- Dynamic Memory Allocation
- Pointer Traps
- Constructor Lab (Bar Codes)
- Olympic Lab

### Introduction to Constructors and Destructors

The concept of creating new data types and designing new data types is the foundation of C++. What constructors do is make sure objects are properly initialized. In C, you're probably used to doing that initialization yourself. What that means though is that you actually have to remember to do the initializing.

When we first looked at types, we used an example of an elevator:

```cpp
class Elevator {
private:
    int floorSelected;
    int floorNumber;
public:
    void initialize();
    void selectFloor(int floor);
    void go();
};
```

The initialize function sets the initial value of the floor selected and the current floor number:

```cpp
void Elevator::initialize() {
    floorSelected = 0;
    floorNumber = 0;
}
```

In C, when you define a variable of a built-in type, you expect the initial value to be garbage. So you must always initialize it before you use it. However, if we forget to initialize an int, the garbage value it contains will still be a legitimate int value, and similarly for the other built-in types.

If we do not call the `Elevator::initialize()` function, however, the initial state of the elevator will probably not be legitimate:

```
Floor # 1001, -47
```

Forgetting an initialization is even more critical if the class contains pointers.

When creating user-defined types, then, it is essential to be able to ensure proper initialization. C++ has a feature to ensure proper initialization, the constructor. The constructor is a special member function which has the same name as the class. If we changed the Elevator::initialize() function to a constructor, it would look like this:

```cpp
class Elevator {
private:
    int floorSelected;
    int floorNumber;
public:
    Elevator();
    void selectFloor(int floor);
    void go();
};
```

Note that a constructor has the same name as the class and has no return value (this is different than a void return value).

Defining a constructor follows the same rules as other member functions:

```cpp
Elevator::Elevator() {
    floorSelected = 0;
    floorNumber = 0;
}
```

The constructor is guaranteed to be called automatically for each object of a class when it is created. In fact, initialization now occurs at the point of definition of the object, before the programmer can even access the object.

```cpp
int main() {
    Elevator e;
    e.selectFloor(7);
    e.go();
    return 0;
}
```

Since the constructor is automatically called, we can guarantee proper initialization of variables. This eliminates a large source of errors and ensures that the object is in a stable state when it's created.

### Default Constructors

A constructor with no arguments is called the *default constructor*.

```cpp
Elevator::Elevator();
```

If no constructor is written for the class, the compiler will supply one that does nothing. However, usually the class design overrides the compiler's default constructor by supplying an explicit default constructor. If a constructor is defined for a class, and is not a default constructor, the default constructor supplied by the compiler ceases to exist.

It's no accident that constructor functions have exactly the same name as the class of which they are members. This is how the compiler knows that they are constructors.

Note that there's no return type with constructors. Why? Since the constructor is automatically called by the system when an object is defined, there's no program to return anything to. Therefore, a return value wouldn't make any sense.

### Constructor Example

```cpp
#include <iostream>
using namespace std;

class Counter {
 private:
  int count;
 public:
  Counter() { count = 0; }
  void incCount() { ++count; }
  int getCount() { return count; }
};

int main() {
 Counter c1, c2;

 cout << "c1 = " << c1.getCount() << endl;
 cout << "c2 = " << c2.getCount() << endl;
 c1.incCount();
 c2.incCount();
 c2.incCount();

 cout << "c1 = " << c1.getCount() << endl;
 cout << "c2 = " << c2.getCount() << endl;
 return 0;
}
```

When an object of type `Counter` is first created, we want its count to be initialized to 0. We could provide a `setCount()` function to do this and call it with an argument of 0, or we could provide a `zeroCount()` function which would always set count to 0. However, such functions would need to be executed every time we created a `Counter` object:

```cpp
Counter c1;
c1.zeroCount();
```

To prove the constructor does its job, let's modify the class:

```cpp
#include <iostream>
using namespace std;
class Counter {
private:
    int count;
public:
    Counter()
    { count = 0; cout << "I'm here. " << endl; }
    void incCount() { ++count; }
    int getCount() { return count; }
};
int main() {
    Counter c1, c2;
    cout << "c1 = " << c1.getCount() << endl;
    cout << "c2 = " << c2.getCount() << endl;
    c1.incCount();
    c2.incCount();
    c2.incCount();
    cout << "c1 = " << c1.getCount() << endl;
    cout << "c2 = " << c2.getCount() << endl;
    return 0;
}
```

Output:
```
I'm here.
I'm here.
c1 = 0;
c2 = 0;
c1 = 1;
c2 = 2;
```
