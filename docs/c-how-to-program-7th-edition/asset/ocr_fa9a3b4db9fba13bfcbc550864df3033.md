Creating a new name with typedef does not create a new type; typedef simply creates a new type name that can then be used in the program as an alias for an existing type name.

> > **Portability Tip 21.2**
> >
> > Synonyms for built-in data types can be created with typedef to make programs more portable. For example, a program can use typedef to create alias Integer for four-byte integers. Integer can then be aliased to int on systems with four-byte integers and can be aliased to long int on systems with two-byte integers where long int values occupy four bytes. Then, you simply declare all four-byte integer variables to be of type Integer.

# ## 21.6 Example: Card Shuffling and Dealing Simulation

The card shuffling and dealing program in Figs. 21.2–21.4 is similar to the one described in Exercise 10.10. This program represents the deck of cards as a vector of structures and uses high-performance shuffling and dealing algorithms.

The constructor (lines 12–32 of Fig. 21.3) initializes the Card vector in order with character strings representing Ace through King of each suit. Function shuffle implements the high-performance shuffling algorithm. The function loops through all 52 cards (subscripts 0 to 51). For each card, a number between 0 and 51 is picked randomly. Next, the current Card structure and the randomly selected Card structure are swapped in the vector. A total of 52 swaps are made in a single pass of the entire vector, and the vector of Card structures is shuffled. Because the Card structures were swapped in place in the vector, the dealing algorithm implemented in function deal requires only one pass of the vector to deal the shuffled cards.

```
```cpp
1  // Fig. 21.2: DeckOfCards.h
2  // Definition of class DeckOfCards that
3  // represents a deck of playing cards.
4  #include <string>
5  #include <vector>
6  using namespace std;
7  
8  // Card structure definition
9  struct Card
10 {
11    string face;
12    string suit;
13 }; // end structure Card
14 
15 // DeckOfCards class definition
16 class DeckOfCards
17 {
18 public:
19    static const int numberOfCards = 52;
20    static const int faces = 13;
21    static const int suits = 4;
22 
```
```

**Fig. 21.2** | Header file for DeckOfCards class. (Part 1 of 2.)