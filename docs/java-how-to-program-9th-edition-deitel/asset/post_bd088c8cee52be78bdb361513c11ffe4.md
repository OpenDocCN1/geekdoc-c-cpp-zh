
Line 16 gets args[0]—a String that specifies the array size—and converts it to an int value that the program uses to create the array in line 17. The static method parseInt of class Integer converts its String argument to an int.

// Fig. 7.21: InitArray.java
// Initializing an array using command-line arguments.

public class InitArray
{
    public static void main( String[] args )
    {
        // check number of command-line arguments
        if ( args.length != 3 )
            System.out.println(
                "Error: Please re-enter the entire command, including\n" +
                "an array size, initial value and increment.");
        else
        {
            // get array size from first command-line argument
            int arrayLength = Integer.parseInt( args[ 0 ] );
            int[] array = new int[ arrayLength ]; // create array

            // get initial value and increment from command-line arguments
            int initialValue = Integer.parseInt( args[ 1 ] );
            int increment = Integer.parseInt( args[ 2 ] );

            // calculate value for each array element
            for ( int counter = 0; counter < array.length; counter++ )
                array[ counter ] = initialValue + increment * counter;

            System.out.printf( "%s%8s\n", "Index", "Value" );

            // display array index and value
            for ( int counter = 0; counter < array.length; counter++ )
                System.out.printf( "%5d%8d\n", counter, array[ counter ] );
        } // end else
    } // end main
} // end class InitArray

```
java InitArray
Error: Please re-enter the entire command, including
an array size, initial value and increment.
```

```
java InitArray 5 0 4
Index    Value
    0       0
    1       4
    2       8
    3      12
    4      16
```

Fig. 7.21 | Initializing an array using command-line arguments. (Part 1 of 2.)

```
java InitArray 8 1 2
Index  Value
0      1
1      3
2      5
3      7
4      9
5      11
6      13
7      15
```

Fig. 7.21 | Initializing an array using command-line arguments. (Part 2 of 2.)

Lines 20–21 convert the args[1] and args[2] command-line arguments to int values and store them in initialValue and increment, respectively. Lines 24–25 calculate the value for each array element.

The output of the first execution shows that the application received an insufficient number of command-line arguments. The second execution uses command-line arguments 5, 0 and 4 to specify the size of the array (5), the value of the first element (0) and the increment of each value in the array (4), respectively. The corresponding output shows that these values create an array containing the integers 0, 4, 8, 12 and 16. The output from the third execution shows that the command-line arguments 8, 1 and 2 produce an array whose 8 elements are the nonnegative odd integers from 1 to 15.

## 7.13 Class Arrays

Class Arrays helps you avoid reinventing the wheel by providing static methods for common array manipulations. These methods include sort for sorting an array (i.e., arranging elements into increasing order), binarySearch for searching an array (i.e., determining whether an array contains a specific value and, if so, where the value is located), equals for comparing arrays and fill for placing values into an array. These methods are overloaded for primitive-type arrays and for arrays of objects. Our focus in this section is on using the built-in capabilities provided by the Java API. Chapter 19, Searching, Sorting and Big O, shows how to implement your own sorting and searching algorithms, which are of great interest to computer-science researchers and students.

Figure 7.22 uses Arrays methods sort, binarySearch, equals and fill, and shows how to copy arrays with class System’s static arraycopy method. In main, line 11 sorts the elements of array doubleArray. The static method sort of class Arrays orders the array’s elements in ascending order by default. We discuss how to sort in descending order later in the chapter. Overloaded versions of sort allow you to sort a specific range of elements. Lines 12–15 output the sorted array.

```
// Fig. 7.22: ArrayManipulations.java
// Arrays class methods and System.arraycopy.
import java.util.Arrays;
```

Fig. 7.22 | Arrays class methods. (Part 1 of 3.)

```
public class ArrayManipulations
{
    public static void main( String[] args )
    {
        // sort doubleArray into ascending order
       double[] doubleArray = { 8.4, 9.3, 0.2, 7.9, 3.4 };
       Arrays.sort( doubleArray );
       System.out.printf( "\ndoubleArray: " );

       for ( double value : doubleArray )
           System.out.printf( "%.1f ", value );

       // fill 10-element array with 7s
       int[] filledIntArray = new int[ 10 ];
       Arrays.fill( filledIntArray, 7 );
       displayArray( filledIntArray, "filledIntArray" );

       // copy array intArray into array intArrayCopy
       int[] intArray = { 1, 2, 3, 4, 5, 6 };
       int[] intArrayCopy = new int[ intArray.length ];
       System.arraycopy( intArray, 0, intArrayCopy, 0, intArray.length );
       displayArray( intArray, "intArray" );
       displayArray( intArrayCopy, "intArrayCopy" );

       // compare intArray and intArrayCopy for equality
       boolean b = Arrays.equals( intArray, intArrayCopy );
       System.out.printf( "\n\nintArray %s intArrayCopy\n",
                        ( b ? "==" : "!=" ) );

       // compare intArray and filledIntArray for equality
       b = Arrays.equals( intArray, filledIntArray );
       System.out.printf( "intArray %s filledIntArray\n",
                        ( b ? "==" : "!=" ) );

       // search intArray for the value 5
       int location = Arrays.binarySearch( intArray, 5 );

       if ( location >= 0 )
           System.out.printf(
               "Found 5 at element %d in intArray\n", location );
       else
           System.out.println( "5 not found in intArray" );

       // search intArray for the value 8763
       location = Arrays.binarySearch( intArray, 8763 );

       if ( location >= 0 )
           System.out.printf(
               "Found 8763 at element %d in intArray\n", location );
       else
           System.out.println( "8763 not found in intArray" );
   } // end main
```

```
// output values in each array
public static void displayArray( int[] array, String description )
{
   System.out.printf( "\n%s: ", description );

   for ( int value : array )
       System.out.printf( "%d ", value );
} // end method displayArray
} // end class ArrayManipulations
```

```
doubleArray: 0.2 3.4 7.9 8.4 9.3
filledIntArray: 7 7 7 7 7 7 7 7 7 7
intArray: 1 2 3 4 5 6
intArrayCopy: 1 2 3 4 5 6

intArray == intArrayCopy
intArray != filledIntArray
Found 5 at element 4 in intArray
8763 not found in intArray
```

Fig. 7.22 | Arrays class methods. (Part 3 of 3.)

Line 19 calls static method fill of class Arrays to populate all 10 elements of filledIntArray with 7s. Overloaded versions of fill allow you to populate a specific range of elements with the same value. Line 20 calls our class’s displayArray method (declared at lines 59–65) to output the contents of filledIntArray.

Line 25 copies the elements of intArray into intArrayCopy. The first argument (intArray) passed to System method arraycopy is the array from which elements are to be copied. The second argument (0) is the index that specifies the starting point in the range of elements to copy from the array. This value can be any valid array index. The third argument (intArrayCopy) specifies the destination array that will store the copy. The fourth argument (0) specifies the index in the destination array where the first copied element should be stored. The last argument specifies the number of elements to copy from the array in the first argument. In this case, we copy all the elements in the array.

Lines 30 and 35 call static method equals of class Arrays to determine whether all the elements of two arrays are equivalent. If the arrays contain the same elements in the same order, the method returns true; otherwise, it returns false.

Lines 40 and 49 call static method binarySearch of class Arrays to perform a binary search on intArray, using the second argument (5 and 8763, respectively) as the key. If value is found, binarySearch returns the index of the element; otherwise, binarySearch returns a negative value. The negative value returned is based on the search key’s insertion point—the index where the key would be inserted in the array if we were performing an insert operation. After binarySearch determines the insertion point, it changes its sign to negative and subtracts 1 to obtain the return value. For example, in Fig. 7.22, the insertion point for the value 8763 is the element with index 6 in the array. Method binarySearch changes the insertion point to -6, subtracts 1 from it and returns the value -7. Subtracting 1 from the insertion point guarantees that method binarySearch returns positive values (>= 0) if and only if the key is found. This return value is useful for inserting elements in a sorted array. Chapter 19 discusses binary searching in detail.
