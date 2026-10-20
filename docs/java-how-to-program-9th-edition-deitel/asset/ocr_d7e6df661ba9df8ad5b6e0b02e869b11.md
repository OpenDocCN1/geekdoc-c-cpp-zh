```
// Fig. 7.12: EnhancedForTest.java
// Using the enhanced for statement to total integers in an array.

public class EnhancedForTest
{
    public static void main( String[] args )
    {
        int[] array = { 87, 68, 94, 100, 83, 78, 85, 91, 76, 87 };
        int total = 0;

        // add each element's value to total
        for ( int number : array )
            total += number;

        System.out.printf( "Total of array elements: %d\n", total );
    } // end main
} // end class EnhancedForTest
```

Total of array elements: 849

Fig. 7.12 | Using the enhanced for statement to total integers in an array.

The enhanced for statement simplifies the code for iterating through an array. Note, however, that the enhanced for statement can be used only to obtain array elements—it cannot be used to modify elements. If your program needs to modify elements, use the traditional counter-controlled for statement.

The enhanced for statement can be used in place of the counter-controlled for statement whenever code looping through an array does not require access to the counter indicating the index of the current array element. For example, totaling the integers in an array requires access only to the element values—the index of each element is irrelevant. However, if a program must use a counter for some reason other than simply to loop through an array (e.g., to print an index number next to each array element value, as in the examples earlier in this chapter), use the counter-controlled for statement.

# 7.7 Passing Arrays to Methods

This section demonstrates how to pass arrays and individual array elements as arguments to methods. To pass an array argument to a method, specify the name of the array without any brackets. For example, if array hourlyTemperatures is declared as

```
double[] hourlyTemperatures = new double[ 24 ];
```

then the method call

```
modifyArray( hourlyTemperatures );
```

passes the reference of array hourlyTemperatures to method modifyArray. Every array object “knows” its own length (via its length field). Thus, when we pass an array object’s reference into a method, we need not pass the array length as an additional argument.