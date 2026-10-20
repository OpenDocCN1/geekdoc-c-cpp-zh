```
// Fig. 7.3: InitArray.java
// Initializing the elements of an array with an array initializer.

public class InitArray
{
    public static void main( String[] args )
    {
        // initializer list specifies the value for each element
        int[] array = { 32, 27, 64, 18, 95, 14, 90, 70, 60, 37 };

        System.out.printf( "%s%8s\n", "Index", "Value" ); // column headings

        // output each array element's value
        for ( int counter = 0; counter < array.length; counter++ )
            System.out.printf( "%5d%8d\n", counter, array[ counter ] );
    } // end main
} // end class InitArray
```

| Index | Value |
| 0 | 32 |
| 1 | 27 |
| 2 | 64 |
| 3 | 18 |
| 4 | 95 |
| 5 | 14 |
| 6 | 90 |
| 7 | 70 |
| 8 | 60 |
| 9 | 37 |

Fig. 7.3 | Initializing the elements of an array with an array initializer.

# Calculating the Values to Store in an Array

The application in Fig. 7.4 creates a 10-element array and assigns to each element one of the even integers from 2 to 20 (2, 4, 6, ..., 20). Then the application displays the array in tabular format. The for statement at lines 12–13 calculates an array element’s value by multiplying the current value of the control variable counter by 2, then adding 2.

```
// Fig. 7.4: InitArray.java
// Calculating the values to be placed into the elements of an array.

public class InitArray
{
    public static void main( String[] args )
    {
        final int ARRAY_LENGTH = 10; // declare constant
        int[] array = new int[ ARRAY_LENGTH ]; // create array

        // calculate value for each array element
        for ( int counter = 0; counter < array.length; counter++ )
            array[ counter ] = 2 + 2 * counter;
```

Fig. 7.4 | Calculating the values to be placed into the elements of an array. (Part I of 2.)