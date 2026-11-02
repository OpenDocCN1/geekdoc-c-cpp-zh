
![](img/d0d3b7423c2d9e5650be79209ea1885d_335_0.png)

**Fig. 7.22** Graphical representation of the `suit` array.

would have to be as large as the largest string. Therefore, considerable memory could be wasted when storing a large number of strings of which most were shorter than the longest string. We use string arrays to represent a deck of cards in the next section.

## 7.11 Case Study: Card Shuffling and Dealing Simulation

In this section, we use random number generation to develop a card shuffling and dealing simulation program. This program can then be used to implement programs that play specific card games. To reveal some subtle performance problems, we’ve intentionally used suboptimal shuffling and dealing algorithms. In this chapter’s exercises and in Chapter 10, we develop more efficient algorithms.

Using the top-down, stepwise refinement approach, we develop a program that will shuffle a deck of 52 playing cards and then deal each of the 52 cards. The top-down approach is particularly useful in attacking larger, more complex problems than you’ve seen in earlier chapters.

### Representing a Deck of Cards as a Two-Dimensional Array

We use a 4-by-13 two-dimensional array `deck` to represent the deck of playing cards (Fig. 7.23). The rows correspond to the suits—row 0 corresponds to hearts, row 1 to diamonds, row 2 to clubs and row 3 to spades. The columns correspond to the face values of the cards—columns 0 through 9 correspond to ace through ten respectively, and columns 10 through 12 correspond to jack, queen and king. We shall load string array `suit` with character strings representing the four suits, and string array `face` with character strings representing the thirteen face values.

### Shuffling the Two-Dimensional Array

This simulated deck of cards may be shuffled as follows. First the array `deck` is cleared to zeros. Then, a row (0–3) and a column (0–12) are each chosen at random. The number 1 is inserted in array element `deck[row][column]` to indicate that this card will be the first one dealt from the shuffled deck. This process continues with the numbers 2, 3, …, 52 being randomly inserted in the deck array to indicate which cards are to be placed second, third, …, and fifty-second in the shuffled deck. As the deck array begins to fill with card numbers, it’s possible that a card will be selected again—i.e., `deck[row][column]` will be nonzero when it’s selected. This selection is simply ignored and other rows and columns are repeatedly chosen at random until an unselected card is found. Eventually, the numbers 1 through 52 will occupy the 52 slots of the deck array. At this point, the deck of cards is fully shuffled.

![](img/d0d3b7423c2d9e5650be79209ea1885d_336_0.png)

**Fig. 7.23** Two-dimensional array representation of a deck of cards.

### Possibility of Indefinite Postponement

This shuffling algorithm can execute indefinitely if cards that have already been shuffled are repeatedly selected at random. This phenomenon is known as indefinite postponement. In this chapter’s exercises, we discuss a better shuffling algorithm that eliminates the possibility of indefinite postponement.

> **Performance Tip 7.3**
> 
> *Sometimes an algorithm that emerges in a “natural” way can contain subtle performance problems, such as indefinite postponement. Seek algorithms that avoid indefinite postponement.*

### Dealing Cards from the Two-Dimensional Array

To deal the first card, we search the array for `deck[row][column]` equal to 1. This is accomplished with nested `for` statements that vary row from 0 to 3 and column from 0 to 12. What card does that element of the array correspond to? The `suit` array has been pre-loaded with the four suits, so to get the suit, we print the character string `suit[row]`. Similarly, to get the face value of the card, we print the character string `face[column]`. We also print the character string `" of "`. Printing this information in the proper order enables us to print each card in the form of `"King of Clubs"`, `"Ace of Diamonds"` and so on.

### Developing the Program’s Logic with Top-Down, Stepwise Refinement

Let’s proceed with the top-down, stepwise refinement process. The top is simply

```
Shuffle and deal 52 cards
```

Our first refinement yields:

- Initialize the suit array
- Initialize the face array
- Initialize the deck array
- Shuffle the deck
- Deal 52 cards

“Shuffle the deck” may be expanded as follows:

```
For each of the 52 cards
    Place card number in randomly selected unoccupied element of deck
```

“Deal 52 cards” may be expanded as follows:

```
For each of the 52 cards
    Find card number in deck array and print face and suit of card
```

Incorporating these expansions yields our complete second refinement:

```
Initialize the suit array
Initialize the face array
Initialize the deck array
For each of the 52 cards
    Place card number in randomly selected unoccupied slot of deck
For each of the 52 cards
    Find card number in deck array and print face and suit of card
```

“Place card number in randomly selected unoccupied slot of deck” may be expanded as:

```
Choose slot of deck randomly
While chosen slot of deck has been previously chosen
    Choose slot of deck randomly
Place card number in chosen slot of deck
```

“Find card number in deck array and print face and suit of card” may be expanded as:

```
For each slot of the deck array
    If slot contains card number
        Print the face and suit of the card
```

Incorporating these expansions yields our third refinement:

```
Initialize the suit array
Initialize the face array
Initialize the deck array
For each of the 52 cards
    Choose slot of deck randomly
    While slot of deck has been previously chosen
        Choose slot of deck randomly
    Place card number in chosen slot of deck
For each of the 52 cards
    For each slot of the deck array
        If slot contains desired card number
            Print the face and suit of the card
```

This completes the refinement process. This program is more efficient if the shuffle and deal portions of the algorithm are combined so that each card is dealt as it’s placed in the deck. We’ve chosen to program these operations separately because normally cards are dealt after they’re shuffled (not while they’re being shuffled).

### Implementing the Card Shuffling and Dealing Program

The card shuffling and dealing program is shown in Fig. 7.24, and a sample execution is shown in Fig. 7.25. Conversion specifier `%s` is used to print strings of characters in the calls to `printf`. The corresponding argument in the `printf` call must be a pointer to `char` (or a `char` array). The format specification `%5s of %-8s` (line 68) prints a character string right justified in a field of five characters followed by `" of "` and a character string left justified in a field of eight characters. The minus sign in `%-8s` signifies left justification.

There’s a weakness in the dealing algorithm. Once a match is found, the two inner `for` statements continue searching the remaining elements of the deck for a match. We correct this deficiency in this chapter’s exercises and in a Chapter 10 case study.

```c
 1 // Fig. 7.24: fig07_24.c
 2 // Card shuffling and dealing.
 3 #include <stdio.h>
 4 #include <stdlib.h>
 5 #include <time.h>
 6
 7 #define SUITS 4
 8 #define FACES 13
 9 #define CARDS 52
10
11 // prototypes
12 void shuffle( unsigned int wDeck[][FACES] ); // shuffling modifies wDeck
13 void deal( unsigned int wDeck[][FACES], const char *wFace[],
14            const char *wSuit[] ); // dealing doesn't modify the arrays
15
16 int main( void )
17 {
18    // initialize deck array
19    unsigned int deck[SUITS][FACES] = { 0 };
20
21    srand( time(NULL) ); // seed random-number generator
22    shuffle( deck ); // shuffle the deck
23
24    // initialize suit array
25    const char *suit[SUITS] =
26       { "Hearts", "Diamonds", "Clubs", "Spades" };
27
28    // initialize face array
29    const char *face[FACES] =
30       { "Ace", "Deuce", "Three", "Four",
31         "Five", "Six", "Seven", "Eight",
32         "Nine", "Ten", "Jack", "Queen", "King" };
33
34    deal( deck, face, suit ); // deal the deck
35 }
36
```

**Fig. 7.24** | Card shuffling and dealing. (Part 1 of 2.)
