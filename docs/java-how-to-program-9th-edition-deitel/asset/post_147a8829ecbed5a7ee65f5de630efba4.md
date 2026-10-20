
```
15      int minuteCompare =
16          time1.getMinute() - time2.getMinute(); // compare minute
17
18      // then test the minute
19      if ( minuteCompare != 0 )
20          return minuteCompare;
21
22      int secondCompare =
23          time1.getSecond() - time2.getSecond(); // compare second
24
25      return secondCompare; // return result of comparing seconds
26  } // end method compare
27 } // end class TimeComparator
```

## Fig. 20.8 | Custom Comparator class that compares two Time2 objects. (Part 2 of 2.)

Class TimeComparator implements interface Comparator, a generic type that takes one type argument (in this case Time2). A class that implements Comparator must declare a compare method that receives two arguments and returns a negative integer if the first argument is less than the second, 0 if the arguments are equal or a positive integer if the first argument is greater than the second. Method compare (lines 7–26) performs comparisons between Time2 objects. Line 9 compares the two hours of the Time2 objects. If the hours are different (line 12), then we return this value. If this value is positive, then the first hour is greater than the second and the first time is greater than the second. If this value is negative, then the first hour is less than the second and the first time is less than the second. If this value is zero, the hours are the same and we must test the minutes (and maybe the seconds) to determine which time is greater.

Figure 20.9 sorts a list using the custom Comparator class TimeComparator. Line 11 creates an ArrayList of Time2 objects. Recall that both ArrayList and List are generic types and accept a type argument that specifies the element type of the collection. Lines 13–17 create five Time2 objects and add them to this list. Line 23 calls method sort, passing it an object of our TimeComparator class (Fig. 20.8).

```
1  // Fig. 20.9: Sort3.java
2  // Collections method sort with a custom Comparator object.
3  import java.util.List;
4  import java.util.ArrayList;
5  import java.util.Collections;
6
7  public class Sort3
8  {
9      public static void main( String[] args )
10     {
11         List< Time2 > list = new ArrayList< Time2 >(); // create List
12
13         list.add( new Time2( 6, 24, 34 ) );
14         list.add( new Time2( 18, 14, 58 ) );
15         list.add( new Time2( 6, 05, 34 ) );
16         list.add( new Time2( 12, 14, 58 ) );
```

## Fig. 20.9 | Collections method sort with a custom Comparator object. (Part 1 of 2.)

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

## 20.7.2 Method shuffle

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

```
68  // output deck
69  public void printCards()
70  {
71      // display 52 cards in two columns
72      for ( int i = 0; i < list.size(); i++ )
73          System.out.printf("%-19s%s", list.get( i ),
74          ( ( i + 1 ) % 4 == 0 ) ? "\n" : "" );
75  } // end method printCards
76  
77  public static void main( String[] args )
78  {
79      DeckOfCards cards = new DeckOfCards();
80      cards.printCards();
81  } // end main
82  } // end class DeckOfCards
```

| Deuce of Clubs | Six of Spades | Nine of Diamonds | Ten of Hearts |
| Three of Diamonds | Five of Clubs | Deuce of Diamonds | Seven of Clubs |
| Three of Spades | Six of Diamonds | King of Clubs | Jack of Hearts |
| Ten of Spades | King of Diamonds | Eight of Spades | Six of Hearts |
| Nine of Clubs | Ten of Diamonds | Eight of Diamonds | Eight of Hearts |
| Ten of Clubs | Five of Hearts | Ace of Clubs | Deuce of Hearts |
| Queen of Diamonds | Ace of Diamonds | Four of Clubs | Nine of Hearts |
| Ace of Spades | Deuce of Spades | Ace of Hearts | Jack of Diamonds |
| Seven of Diamonds | Three of Hearts | Four of Spades | Four of Diamonds |
| Seven of Spades | King of Hearts | Seven of Hearts | Five of Diamonds |
| Eight of Clubs | Three of Clubs | Queen of Clubs | Queen of Spades |
| Six of Clubs | Nine of Spades | Four of Hearts | Jack of Clubs |
| Five of Spades | King of Spades | Jack of Spades | Queen of Hearts |

Fig. 20.10 | Card shuffling and dealing with Collections method shuffle. (Part 3 of 3.)

Lines 55–62 populate the deck array with cards that have unique face and suit combinations. Both Face and Suit are public static enum types of class Card. To use these enum types outside of class Card, you must qualify each enum’s type name with the name of the class in which it resides (i.e., Card) and a dot (.) separator. Hence, lines 55 and 57 use Card.Suit and Card.Face to declare the control variables of the for statements. Recall that method values of an enum type returns an array that contains all the constants of the enum type. Lines 55–62 use enhanced for statements to construct 52 new Cards.

The shuffling occurs in line 65, which calls static method shuffle of class Collections to shuffle the elements of the array. Method shuffle requires a List argument, so we must obtain a List view of the array before we can shuffle it. Line 64 invokes static method asList of class Arrays to get a List view of the deck array.

Method printCards (lines 69–75) displays the deck of cards in four columns. In each iteration of the loop, lines 73–74 output a card left justified in a 19-character field followed by either a newline or an empty string based on the number of cards output so far. If the number of cards is divisible by 4, a newline is output; otherwise, the empty string is output.

## 20.7.3 Methods reverse, fill, copy, max and min

Class Collections provides methods for reversing, filling and copying Lists. Collections method reverse reverses the order of the elements in a List, and method fill

value. Method binarySearch determines this negative value by first calculating the insertion point and making its sign negative. Then, binarySearch subtracts 1 from the insertion point to obtain the return value, which guarantees that method binarySearch returns positive numbers (>= 0) if and only if the object is found. If multiple elements in the list match the search key, there’s no guarantee which one will be located first. Figure 20.12 uses method binarySearch to search for a series of strings in an ArrayList.

```
// Fig. 20.12: BinarySearchTest.java
// Collections method binarySearch.
import java.util.List;
import java.util.Arrays;
import java.util.Collections;
import java.util.ArrayList;

public class BinarySearchTest
{
    public static void main( String[] args )
    {
        // create an ArrayList< String > from the contents of colors array
        String[] colors = { "red", "white", "blue", "black", "yellow",
            "purple", "tan", "pink" };
        List< String > list =
            new ArrayList< String >( Arrays.asList( colors ) );

        Collections.sort( list ); // sort the ArrayList
        System.out.printf( "Sorted ArrayList: %s\n", list );

        // search list for various values
        printSearchResults( list, colors[ 3 ] ); // first item
        printSearchResults( list, colors[ 0 ] ); // middle item
        printSearchResults( list, colors[ 7 ] ); // last item
        printSearchResults( list, "aqua" ); // below lowest
        printSearchResults( list, "gray" ); // does not exist
        printSearchResults( list, "teal" ); // does not exist
    } // end main

    // perform search and display result
    private static void printSearchResults(
        List< String > list, String key )
    {
        int result = 0;

        System.out.printf( "\nSearching for: %s\n", key );
        result = Collections.binarySearch( list, key );

        if ( result >= 0 )
            System.out.printf( "Found at index %d\n", result );
        else
            System.out.printf( "Not Found (%d)\n", result );
    } // end method printSearchResults
} // end class BinarySearchTest
```
