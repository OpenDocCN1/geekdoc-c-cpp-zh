
Next, the algorithm checks whether 81 (the middle element of the remainder of the array) matches the search key. The search key (65) is smaller than 81, so 81 is discarded along with the elements larger than 81. After just two tests, the algorithm has narrowed the number of values to check to only three (56, 65 and 77). It then checks 65 (which indeed matches the search key) and returns the index of the array element containing 65. This algorithm required just three comparisons to determine whether the search key matched an element of the array. Using a linear search algorithm would have required 10 comparisons. [Note: In this example, we’ve chosen to use an array with 15 elements so that there will always be an obvious middle element in the array. With an even number of elements, the middle of the array lies between two elements. We implement the algorithm to choose the higher of those two elements.]

## Binary Search Implementation

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

```
27    int low = 0; // low end of the search area
28    int high = data.length - 1; // high end of the search area
29    int middle = ( low + high + 1 ) / 2; // middle element
30    int location = -1; // return value; -1 if not found
31
32    do // loop to search for element
33    {
34        // print remaining elements of array
35        System.out.print( remainingElements( low, high ) );
36
37        // output spaces for alignment
38        for ( int i = 0; i < middle; i++ )
39            System.out.print( "   " );
40        System.out.println( " * " ); // indicate current middle
41
42        // if the element is found at the middle
43        if ( searchElement == data[ middle ] )
44            location = middle; // location is the current middle
45
46        // middle element is too high
47        else if ( searchElement < data[ middle ] )
48            high = middle - 1; // eliminate the higher half
49        else // middle element is too low
50            low = middle + 1; // eliminate the lower half
51
52        middle = ( low + high + 1 ) / 2; // recalculate the middle
53    } while ( ( low <= high ) && ( location == -1 ) );
54
55    return location; // return location of search key
56 } // end method binarySearch
57
58    // method to output certain values in array
59    public String remainingElements( int low, int high )
60    {
61        StringBuilder temporary = new StringBuilder();
62
63        // output spaces for alignment
64        for ( int i = 0; i < low; i++ )
65            temporary.append( "   " );
66
67        // output elements left in array
68        for ( int i = low; i <= high; i++ )
69            temporary.append( data[ i ] + " " );
70
71        temporary.append( "\n" );
72        return temporary.toString();
73    } // end method remainingElements
74
75    // method to output values in array
76    public String toString()
77    {
```

Fig. 19.4 | Class that contains an array of random integers and a method that uses binary search to find an integer. (Part 2 of 3.)

```
78        return remainingElements( 0, data.length - 1 );
79    } // end method toString
80 } // end class BinaryArray
```

Fig. 19.4 | Class that contains an array of random integers and a method that uses binary search to find an integer. (Part 3 of 3.)

Lines 25–56 declare method binarySearch. The search key is passed into parameter searchElement (line 25). Lines 27–29 calculate the low end index, high end index and middle index of the portion of the array that the program is currently searching. At the beginning of the method, the low end is 0, the high end is the length of the array minus 1 and the middle is the average of these two values. Line 30 initializes the location of the element to -1—the value that will be returned if the element is not found. Lines 32–53 loop until low is greater than high (this occurs when the element is not found) or location does not equal -1 (indicating that the search key was found). Line 43 tests whether the value in the middle element is equal to searchElement. If this is true, line 44 assigns middle to location. Then the loop terminates and location is returned to the caller. Each iteration of the loop tests a single value (line 43) and eliminates half of the remaining values in the array (line 48 or 50).

Figure 19.5 performs a binary search using the search key the user enters to determine whether it matches an element in the array. The first line of output from this program is the array of ints, in increasing order. When the user instructs the program to search for 23, the program first tests the middle element, which is 42 (as indicated by *). The search key is less than 42, so the program eliminates the second half of the array and tests the middle element from the first half. The search key is smaller than 34, so the program eliminates the second half of the array, leaving only three elements. Finally, the program checks 23 (which matches the search key) and returns the index 1.

```
1 // Fig. 19.5: BinarySearchTest.java
2 // Use binary search to locate an item in an array.
3 import java.util.Scanner;
4 
5 public class BinarySearchTest
6 {
7     public static void main( String[] args )
8     {
9         // create Scanner object to input data
10        Scanner input = new Scanner( System.in );
11
12        int searchInt; // search key
13        int position; // location of search key in array
14
15        // create array and output it
16        BinaryArray searchArray = new BinaryArray( 15 );
17        System.out.println( searchArray );
18
```

Fig. 19.5 | Use binary search to locate an item in an array (* in the output marks the middle element). (Part 1 of 3.)

```
19      // get input from user
20      System.out.print(
21      "Please enter an integer value (-1 to quit): " );
22      searchInt = input.nextInt(); // read an int from user
23      System.out.println();
24
25      // repeatedly input an integer; -1 terminates the program
26      while ( searchInt != -1 )
27      {
28          // use binary search to try to find integer
29          position = searchArray.binarySearch( searchInt );
30
31          // return value of -1 indicates integer was not found
32          if ( position == -1 )
33              System.out.println( "The integer " + searchInt +
34              " was not found.\n" );
35          else
36              System.out.println( "The integer " + searchInt +
37              " was found in position " + position + ".\n" );
38
39          // get input from user
40          System.out.print(
41          "Please enter an integer value (-1 to quit): " );
42          searchInt = input.nextInt(); // read an int from user
43          System.out.println();
44      } // end while
45      } // end main
46  } // end class BinarySearchTest
```

```
13 23 24 34 35 36 38 42 47 51 68 74 75 85 97

Please enter an integer value (-1 to quit): 23

13 23 24 34 35 36 38 42 47 51 68 74 75 85 97
                    *
13 23 24 34 35 36 38
        *
13 23 24
    *
The integer 23 was found in position 1.

Please enter an integer value (-1 to quit): 75

13 23 24 34 35 36 38 42 47 51 68 74 75 85 97
                    *
                47 51 68 74 75 85 97
                        *
                            75 85 97
                                *
                                75
                                *
The integer 75 was found in position 12.
```

Fig. 19.5 | Use binary search to locate an item in an array (* in the output marks the middle element). (Part 2 of 3.)
