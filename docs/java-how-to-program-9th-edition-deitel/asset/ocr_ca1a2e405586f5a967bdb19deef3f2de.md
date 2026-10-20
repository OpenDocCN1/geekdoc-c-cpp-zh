Next, the algorithm checks whether 81 (the middle element of the remainder of the array) matches the search key. The search key (65) is smaller than 81, so 81 is discarded along with the elements larger than 81. After just two tests, the algorithm has narrowed the number of values to check to only three (56, 65 and 77). It then checks 65 (which indeed matches the search key) and returns the index of the array element containing 65. This algorithm required just three comparisons to determine whether the search key matched an element of the array. Using a linear search algorithm would have required 10 comparisons. [Note: In this example, we’ve chosen to use an array with 15 elements so that there will always be an obvious middle element in the array. With an even number of elements, the middle of the array lies between two elements. We implement the algorithm to choose the higher of those two elements.]

# Binary Search Implementation

Figure 19.4 declares class BinaryArray. This class is similar to LinearArray—it has two private instance variables, a constructor, a search method (binarySearch), a remainingElements method and a toString method. Lines 13–22 declare the constructor. After the array has been initialized with random ints from 10–99 (lines 18–19), line 21 calls the Arrays.sort method on the array data. The sort method is a static method of class Arrays that sorts the elements in an array in ascending order by default; an overloaded version of this method allows you to change the sorting order. Recall that the binary search algorithm will work only on a sorted array.

```
1  // Fig. 19.4: BinaryArray.java
2  // Class that contains an array of random integers and a method
3  // that uses binary search to find an integer.
4  import java.util.Random;
5  import java.util.Arrays;
6
7  public class BinaryArray
8  {
9      private int[] data; // array of values
10     private static final Random generator = new Random();
11
12     // create array of given size and fill with random integers
13     public BinaryArray( int size )
14     {
15         data = new int[ size ]; // create space for array
16
17         // fill array with random ints in range 10-99
18         for ( int i = 0; i < size; i++ )
19             data[ i ] = 10 + generator.nextInt( 90 );
20
21         Arrays.sort( data );
22     } // end BinaryArray constructor
23
24     // perform a binary search on the data
25     public int binarySearch( int searchElement )
26     {
```

Fig. 19.4 | Class that contains an array of random integers and a method that uses binary search to find an integer. (Part 1 of 3.)