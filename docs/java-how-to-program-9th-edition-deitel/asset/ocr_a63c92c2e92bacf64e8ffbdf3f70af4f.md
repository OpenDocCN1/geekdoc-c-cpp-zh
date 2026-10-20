```
// Fig. 7.6: BarChart.java
// Bar chart printing program.

public class BarChart
{
    public static void main( String[] args )
    {
        int[] array = { 0, 0, 0, 0, 0, 0, 1, 2, 4, 2, 1 };

        System.out.println( "Grade distribution:" );

        // for each array element, output a bar of the chart
        for ( int counter = 0; counter < array.length; counter++ )
        {
            // output bar label ( "00-09: ", ..., "90-99: " "100: " )
            if ( counter == 10 )
                System.out.printf( "%5d: ", 100 );
            else
                System.out.printf( "%02d-%02d: ",
                    counter * 10, counter * 10 + 9 );

            // print bar of asterisks
            for ( int stars = 0; stars < array[ counter ]; stars++ )
                System.out.print( "*" );

            System.out.println(); // start a new line of output
        } // end outer for
    } // end main
} // end class BarChart
```

```
Grade distribution:
00-09:
10-19:
20-29:
30-39:
40-49:
50-59:
60-69: *
70-79: **
80-89: ****
90-99: **
    100: *
```

# Fig. 7.6 | Bar chart printing program.

The application reads the numbers from the array and graphs the information as a bar chart. It displays each grade range followed by a bar of asterisks indicating the number of grades in that range. To label each bar, lines 16–20 output a grade range (e.g., "70-79: ") based on the current value of counter. When counter is 10, line 17 outputs 100 with a field width of 5, followed by a colon and a space, to align the label "100: " with the other bar labels. The nested for statement (lines 23–24) outputs the bars. Note the loop-continuation condition at line 23 (stars < array[counter]). Each time the program reaches the inner for, the loop counts from 0 up to array[counter], thus using a value in array