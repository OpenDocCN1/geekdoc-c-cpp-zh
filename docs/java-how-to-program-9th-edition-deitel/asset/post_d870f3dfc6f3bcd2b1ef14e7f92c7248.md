
## Two-Dimensional Array Example: Displaying Element Values

Figure 7.17 demonstrates initializing two-dimensional arrays with array initializers and using nested for loops to traverse the arrays (i.e., manipulate every element of each array). Class InitArray's main declares two arrays. The declaration of array1 (line 9) uses nested array initializers of the same length to initialize the first row to the values 1, 2 and 3, and the second row to the values 4, 5 and 6. The declaration of array2 (line 10) uses nested initializers of different lengths. In this case, the first row is initialized to two elements with the values 1 and 2, respectively. The second row is initialized to one element with the value 3. The third row is initialized to three elements with the values 4, 5 and 6, respectively.

```
// Fig. 7.17: InitArray.java
// Initializing two-dimensional arrays.

public class InitArray
{
    // create and output two-dimensional arrays
    public static void main( String[] args )
    {
        int[][] array1 = { { 1, 2, 3 }, { 4, 5, 6 } };
        int[][] array2 = { { 1, 2 }, { 3 }, { 4, 5, 6 } };

        System.out.println( "Values in array1 by row are" );
        outputArray( array1 ); // displays array1 by row

        System.out.println( "\nValues in array2 by row are" );
        outputArray( array2 ); // displays array2 by row
    } // end main

    // output rows and columns of a two-dimensional array
    public static void outputArray( int[][] array )
    {
        // loop through array's rows
        for ( int row = 0; row < array.length; row++ )
        {
            // loop through columns of current row
            for ( int column = 0; column < array[ row ].length; column++ )
                System.out.printf( "%d  ", array[ row ][ column ] );

            System.out.println(); // start new line of output
        } // end outer for
    } // end method outputArray
} // end class InitArray
```

```
Values in array1 by row are
1  2  3
4  5  6

Values in array2 by row are
1  2
3
4  5  6
```

Fig. 7.17 | Initializing two-dimensional arrays.

Lines 13 and 16 call method outputArray (lines 20–31) to output the elements of array1 and array2, respectively. Method outputArray’s parameter—int[][] array—indicates that the method receives a two-dimensional array. The for statement (lines 23–30) outputs the rows of a two-dimensional array. In the loop-continuation condition of the outer for statement, the expression array.length determines the number of rows in the array. In the inner for statement, the expression array[row].length determines the number of columns in the current row of the array. The inner for statement’s condition enables the loop to determine the exact number of columns in each row.

## Common Multidimensional-Array Manipulations Performed with for Statements

Many common array manipulations use for statements. As an example, the following for statement sets all the elements in row 2 of array a in Fig. 7.16 to zero:

```
for ( int column = 0; column < a[ 2 ].length; column++)
    a[ 2 ][ column ] = 0;
```

We specified row 2; therefore, we know that the first index is always 2 (0 is the first row, and 1 is the second row). This for loop varies only the second index (i.e., the column index). If row 2 of array a contains four elements, then the preceding for statement is equivalent to the assignment statements

```
a[ 2 ][ 0 ] = 0;
a[ 2 ][ 1 ] = 0;
a[ 2 ][ 2 ] = 0;
a[ 2 ][ 3 ] = 0;
```

The following nested for statement totals the values of all the elements in array a:

```
int total = 0;
for ( int row = 0; row < a.length; row++ )
{
    for ( int column = 0; column < a[ row ].length; column++ )
        total += a[ row ][ column ];
} // end outer for
```

These nested for statements total the array elements one row at a time. The outer for statement begins by setting the row index to 0 so that the first row’s elements can be totaled by the inner for statement. The outer for then increments row to 1 so that the second row can be totaled. Then, the outer for increments row to 2 so that the third row can be totaled. The variable total can be displayed when the outer for statement terminates. In the next example, we show how to process a two-dimensional array in a similar manner using nested enhanced for statements.

## 7.10 Case Study: Class GradeBook Using a Two-Dimensional Array

In Section 7.8, we presented class GradeBook (Fig. 7.14), which used a one-dimensional array to store student grades on a single exam. In most semesters, students take several exams. Professors are likely to want to analyze grades across the entire semester, both for a single student and for the class as a whole.

```
// perform various operations on the data
public void processGrades()
{
    // output grades array
    outputGrades();

    // call methods getMinimum and getMaximum
    System.out.printf( "\n%s %d\n%s %d\n\n",
        "Lowest grade in the grade book is", getMinimum(),
        "Highest grade in the grade book is", getMaximum() );

    // output grade distribution chart of all grades on all tests
    outputBarChart();
} // end method processGrades

// find minimum grade
public int getMinimum()
{
    // assume first element of grades array is smallest
    int lowGrade = grades[ 0 ][ 0 ];

    // loop through rows of grades array
    for ( int[] studentGrades : grades )
    {
        // loop through columns of current row
        for ( int grade : studentGrades )
        {
            // if grade less than lowGrade, assign it to lowGrade
            if ( grade < lowGrade )
                lowGrade = grade;
        } // end inner for
    } // end outer for

    return lowGrade; // return lowest grade
} // end method getMinimum

// find maximum grade
public int getMaximum()
{
    // assume first element of grades array is largest
    int highGrade = grades[ 0 ][ 0 ];

    // loop through rows of grades array
    for ( int[] studentGrades : grades )
    {
        // loop through columns of current row
        for ( int grade : studentGrades )
        {
            // if grade greater than highGrade, assign it to highGrade
            if ( grade > highGrade )
                highGrade = grade;
        } // end inner for
    } // end outer for

return highGrade; // return highest grade
} // end method getMaximum

// determine average grade for particular set of grades
public double getAverage( int[] setOfGrades )
{
    int total = 0; // initialize total

    // sum grades for one student
    for ( int grade : setOfGrades )
        total += grade;

    // return average of grades
    return (double) total / setOfGrades.length;
} // end method getAverage

// output bar chart displaying overall grade distribution
public void outputBarChart()
{
    System.out.println( "Overall grade distribution:" );

    // stores frequency of grades in each range of 10 grades
    int[] frequency = new int[ 11 ];

    // for each grade in GradeBook, increment the appropriate frequency
    for ( int[] studentGrades : grades )
    {
        for ( int grade : studentGrades )
            ++frequency[ grade / 10 ];
    } // end outer for

    // for each grade frequency, print bar in chart
    for ( int count = 0; count < frequency.length; count++ )
    {
        // output bar label ( "00-09: ", ..., "90-99: ", "100: " )
        if ( count == 10 )
            System.out.printf( "%5d: ", 100 );
        else
            System.out.printf( "%02d-%02d: ",
                count * 10, count * 10 + 9 );

        // print bar of asterisks
        for ( int stars = 0; stars < frequency[ count ]; stars++ )
            System.out.print( "*" );

        System.out.println(); // start a new line of output
    } // end outer for
} // end method outputBarChart

// output the contents of the grades array
public void outputGrades()
{
142 System.out.println( "The grades are:\n" );
143 System.out.print( "                " ); // align column heads
144
145 // create a column heading for each of the tests
146 for ( int test = 0; test < grades[ 0 ].length; test++ )
147     System.out.printf( "Test %d  ", test + 1 );
148
149 System.out.println( "Average" ); // student average column heading
150
151 // create rows/columns of text representing array grades
152 for ( int student = 0; student < grades.length; student++ )
153 {
154     System.out.printf( "Student %2d", student + 1 );
155
156     for ( int test : grades[ student ] ) // output student's grades
157         System.out.printf( "%8d", test );
158
159     // call method getAverage to calculate student's average grade;
160     // pass row of grades as the argument to getAverage
161     double average = getAverage( grades[ student ] );
162     System.out.printf( "%9.2f\n", average );
163 } // end outer for
164 } // end method outputGrades
165 } // end class GradeBook
```

Fig. 7.18 | GradeBook class using a two-dimensional array to store grades. (Part 4 of 4.)

## Methods getMinimum and getMaximum

Methods getMinimum, getMaximum, outputBarChart and outputGrades each loop through array grades by using nested for statements—for example, the nested enhanced for statement from the declaration of method getMinimum (lines 58–67). The outer enhanced for statement iterates through the two-dimensional array grades, assigning successive rows to parameter studentGrades on successive iterations. The square brackets following the parameter name indicate that studentGrades refers to a one-dimensional int array—namely, a row in array grades containing one student’s grades. To find the lowest overall grade, the inner for statement compares the elements of the current one-dimensional array studentGrades to variable lowGrade. For example, on the first iteration of the outer for, row 0 of grades is assigned to parameter studentGrades. The inner enhanced for statement then loops through studentGrades and compares each grade value with lowGrade. If a grade is less than lowGrade, lowGrade is set to that grade. On the second iteration of the outer enhanced for statement, row 1 of grades is assigned to studentGrades, and the elements of this row are compared with variable lowGrade. This repeats until all rows of grades have been traversed. When execution of the nested statement is complete, lowGrade contains the lowest grade in the two-dimensional array. Method getMaximum works similarly to method getMinimum.

## Method outputBarChart

Method outputBarChart in Fig. 7.18 is nearly identical to the one in Fig. 7.14. However, to output the overall grade distribution for a whole semester, the method here uses nested enhanced for statements (lines 115–119) to create the one-dimensional array frequency
