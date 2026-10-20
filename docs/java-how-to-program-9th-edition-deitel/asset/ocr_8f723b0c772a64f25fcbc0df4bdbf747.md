```
public static void main( String[] args )
{
    // create object to perform selection sort
    SelectionSort sortArray = new SelectionSort( 10 );

    System.out.println( "Unsorted array:" );
    System.out.println( sortArray + "\n" ); // print unsorted array

    sortArray.sort(); // sort array

    System.out.println( "Sorted array:" );
    System.out.println( sortArray ); // print sorted array
} // end main
} // end class SelectionSortTest
```

Unsorted array:
[61, 87, 80, 58, 40, 50, 20, 13, 71, 45]
after pass  1: 13  87  80  58  40  50  20  61* 71  45
            --
after pass  2: 13  20  80  58  40  50  87* 61  71  45
            --  --
after pass  3: 13  20  40  58  80* 50  87  61  71  45
            --  --  --
after pass  4: 13  20  40  45  80  50  87  61  71  58*
            --  --  --  --
after pass  5: 13  20  40  45  50  80* 87  61  71  58
            --  --  --  --  --
after pass  6: 13  20  40  45  50  58  87  61  71  80*
            --  --  --  --  --  --
after pass  6: 13  20  40  45  50  58  87  61  71  80*
            --  --  --  --  --  --
after pass  7: 13  20  40  45  50  58  61  87* 71  80
            --  --  --  --  --  --  --
after pass  8: 13  20  40  45  50  58  61  71  87* 80
            --  --  --  --  --  --  --  --
after pass  9: 13  20  40  45  50  58  61  71  80  87*
            --  --  --  --  --  --  --  --  --
Sorted array:
[13, 20, 40, 45, 50, 58, 61, 71, 80, 87]

Fig. 19.7 | Testing the selection sort class. (Part 2 of 2.)

# Efficiency of the Selection Sort

The selection sort algorithm runs in O(n²) time. The sort method in lines 23–40 of Fig. 19.6, which implements the selection sort algorithm, contains two for loops. The outer for loop (lines 28–39) iterates over the first n − 1 elements in the array, swapping the smallest remaining item into its sorted position. The inner for loop (lines 33–35) iterates over each