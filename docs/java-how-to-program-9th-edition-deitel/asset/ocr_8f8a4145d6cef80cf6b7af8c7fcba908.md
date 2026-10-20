Line 16 gets args[0]—a String that specifies the array size—and converts it to an int value that the program uses to create the array in line 17. The static method parseInt of class Integer converts its String argument to an int.

```
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