index for array frequency. In line 14, the calculation inside the square brackets evaluates first to determine which element of the array to increment, then the ++ operator adds one to that element. We also replaced lines 50–52 from Fig. 6.7 by looping through array frequency to output the results (lines 19–20).

# Using Arrays to Analyze Survey Results

Our next example uses arrays to summarize data collected in a survey. Consider the following problem statement:

> Twenty students were asked to rate on a scale of 1 to 5 the quality of the food in the student cafeteria, with 1 being "awful" and 5 being "excellent." Place the 20 responses in an integer array and determine the frequency of each rating.

This is a typical array-processing application (Fig. 7.8). We wish to summarize the number of responses of each type (that is, 1–5). Array responses (lines 9–10) is a 20-element integer array containing the students’ survey responses. The last value in the array is intentionally an incorrect response (14). When a Java program executes, array element indices are checked for validity—all indices must be greater than or equal to 0 and less than the length of the array. Any attempt to access an element outside that range of indices results in a runtime error that’s known as an ArrayIndexOutOfBoundsException. At the end of this section, we’ll discuss the invalid response value, demonstrate array bounds checking and introduce Java’s exception-handling mechanism, which can be used to detect and handle an ArrayIndexOutOfBoundsException.

```
// Fig. 7.8: StudentPoll.java
// Poll analysis program.

public class StudentPoll
{
    public static void main( String[] args )
    {
        // student response array (more typically, input at runtime)
        int[] responses = { 1, 2, 5, 4, 3, 5, 2, 1, 3, 3, 1, 4, 3, 3, 3,
            2, 3, 3, 2, 14 };
        int[] frequency = new int[ 6 ]; // array of frequency counters

        // for each answer, select responses element and use that value
        // as frequency index to determine element to increment
        for ( int answer = 0; answer < responses.length; answer++ )
        {
            try
            {
                ++frequency[ responses[ answer ] ];
            } // end try
            catch ( ArrayIndexOutOfBoundsException e )
            {
                System.out.println( e );
                System.out.printf( "    responses[%d] = %d\n\n",
                    answer, responses[ answer ] );
            } // end catch
        } // end for
```