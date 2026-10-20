```
17      list.add( new Time2( 6, 24, 22 ) );
18
19      // output List elements
20      System.out.printf( "Unsorted array elements:\n%s\n", list );
21
22      // sort in order using a comparator
23      Collections.sort( list, new TimeComparator() );
24
25      // output List elements
26      System.out.printf( "Sorted list elements:\n%s\n", list );
27    } // end main
28  } // end class Sort3
```

Unsorted array elements:
[6:24:34 AM, 6:14:58 PM, 6:05:34 AM, 12:14:58 PM, 6:24:22 AM]
Sorted list elements:
[6:05:34 AM, 6:24:22 AM, 6:24:34 AM, 12:14:58 PM, 6:14:58 PM]

Fig. 20.9 | Collections method sort with a custom Comparator object. (Part 2 of 2.)

# 20.7.2 Method shuffle

Method shuffle randomly orders a List’s elements. Chapter 7 presented a card shuffling and dealing simulation that shuffled a deck of cards with a loop. Figure 20.10 uses method shuffle to shuffle a deck of Card objects that might be used in a card-game simulator.

Class Card (lines 8–41) represents a card in a deck of cards. Each Card has a face and a suit. Lines 10–12 declare two enum types—Face and Suit—which represent the face and the suit of the card, respectively. Method toString (lines 37–40) returns a String containing the face and suit of the Card separated by the string " of ". When an enum constant is converted to a string, the constant’s identifier is used as the string representation. Normally we would use all uppercase letters for enum constants. In this example, we chose to use capital letters for only the first letter of each enum constant because we want the card to be displayed with initial capital letters for the face and the suit (e.g., "Ace of Spades").

```
1  // Fig. 20.10: DeckOfCards.java
2  // Card shuffling and dealing with Collections method shuffle.
3  import java.util.List;
4  import java.util.Arrays;
5  import java.util.Collections;
6
7  // class to represent a Card in a deck of cards
8  class Card
9  {
10     public static enum Face { Ace, Deuce, Three, Four, Five, Six,
11         Seven, Eight, Nine, Ten, Jack, Queen, King };
12     public static enum Suit { Clubs, Diamonds, Hearts, Spades };
13
14     private final Face face; // face of card
15     private final Suit suit; // suit of card
```

Fig. 20.10 | Card shuffling and dealing with Collections method shuffle. (Part 1 of 3.)