# Software Engineering Observation 20.4

The collections framework methods are polymorphic. That is, each can operate on objects that implement specific interfaces, regardless of the underlying implementations.

# 20.7.1 Method sort

Method sort sorts the elements of a List, which must implement the Comparable interface. The order is determined by the natural order of the elements’ type as implemented by a compareTo method. Method compareTo is declared in interface Comparable and is sometimes called the natural comparison method. The sort call may specify as a second argument a Comparator object that determines an alternative ordering of the elements.

# Sorting in Ascending Order

Figure 20.6 uses Collections method sort to order the elements of a List in ascending order (line 17). Recall that List is a generic type and accepts one type argument that specifies the list element type—line 14 creates list as a List of Strings. Lines 15 and 20 each use an implicit call to the list’s toString method to output the list contents in the format shown in the output.

```
// Fig. 20.6: Sort1.java
// Collections method sort.
import java.util.List;
import java.util.Arrays;
import java.util.Collections;

public class Sort1
{
    public static void main( String[] args )
    {
        String[] suits = { "Hearts", "Diamonds", "Clubs", "Spades" };

        // Create and display a list containing the suits array elements
        List< String > list = Arrays.asList( suits ); // create List
        System.out.printf( "Unsorted array elements: %s\n", list );

        Collections.sort( list ); // sort ArrayList

        // output list
        System.out.printf( "Sorted array elements: %s\n", list );
    } // end main
} // end class Sort1
```

Unsorted array elements: [Hearts, Diamonds, Clubs, Spades]
Sorted array elements: [Clubs, Diamonds, Hearts, Spades]

Fig. 20.6 | Collections method sort.

# Sorting in Descending Order

Figure 20.7 sorts the same list of strings used in Fig. 20.6 in descending order. The example introduces the Comparator interface, which is used for sorting a Collection’s elements in a different order. Line 18 calls Collections’s method sort to order the List in de-