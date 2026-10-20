
// multiply each element of an array by 2
public static void modifyArray( int[] array2 )
{
    for ( int counter = 0; counter < array2.length; counter++ )
        array2[ counter ] *= 2;
} // end method modifyArray

// multiply argument by 2
public static void modifyElement( int element )
{
    element *= 2;
    System.out.printf(
        "Value of element in modifyElement: %d\n", element );
} // end method modifyElement

} // end class PassArray

Effects of passing reference to entire array:
The values of the original array are:
  1  2  3  4  5

The values of the modified array are:
  2  4  6  8  10

Effects of passing array element value:
array[3] before modifyElement: 8
Value of element in modifyElement: 16
array[3] after modifyElement: 8

Fig. 7.13 | Passing arrays and individual array elements to methods. (Part 2 of 2.)

The enhanced for statement at lines 16–17 outputs the five int elements of array. Line 19 invokes method modifyArray, passing array as an argument. Method modifyArray (lines 36–40) receives a copy of array’s reference and uses the reference to multiply each of array’s elements by 2. To prove that array’s elements were modified, lines 23–24 output the five elements of array again. As the output shows, method modifyArray doubled the value of each element. We could not use the enhanced for statement in lines 38–39 because we’re modifying the array’s elements.

Figure 7.13 next demonstrates that when a copy of an individual primitive-type array element is passed to a method, modifying the copy in the called method does not affect the original value of that element in the calling method’s array. Lines 26–28 output the value of array[3] before invoking method modifyElement. Remember that the value of this element is now 8 after it was modified in the call to modifyArray. Line 30 calls method modifyElement and passes array[3] as an argument. Remember that array[3] is actually one int value (8) in array. Therefore, the program passes a copy of the value of array[3]. Method modifyElement (lines 43–48) multiplies the value received as an argument by 2, stores the result in its parameter element, then outputs the value of element (16). Since method parameters, like local variables, cease to exist when the method in which they’re declared completes execution, the method parameter element is destroyed when method modifyElement terminates. When the program returns control to main, lines 31–32 output the unmodified value of array[3] (i.e., 8).

dent grades. But this would make the code to total the grades and determine the class average cumbersome, and the class would not be able to process any more than 10 grades at a time. We solve this problem by storing grades in an array.

## Storing Student Grades in an Array in Class GradeBook

Class GradeBook (Fig. 7.14) uses an array of ints to store several students’ grades on a single exam. This eliminates the need to repeatedly input the same set of grades. Array grades is declared as an instance variable (line 7), so each GradeBook object maintains its own set of grades. The constructor (lines 10–14) has two parameters—the name of the course and an array of grades. When an application (e.g., class GradeBookTest in Fig. 7.15) creates a GradeBook object, the application passes an existing int array to the constructor, which assigns the array’s reference to instance variable grades (line 13). The grades array’s size is determined by the length of the array that’s passed to the constructor. Thus, a GradeBook object can process a variable number of grades. The grade values in the passed array could have been input from a user or read from a file on disk (as discussed in Chapter 17). In our test application, we initialize an array with grade values (Fig. 7.15, line 10). Once the grades are stored in instance variable grades of class GradeBook, all the class’s methods can access the elements of grades as often as needed to perform various calculations.

Method processGrades (lines 37–51) contains a series of method calls that output a report summarizing the grades. Line 40 calls method outputGrades to print the contents of the array grades. Lines 134–136 in method outputGrades use a for statement to output the students’ grades. A counter-controlled for must be used in this case, because lines 135–136 use counter variable student’s value to output each grade next to a particular student number (see output in Fig. 7.15). Although array indices start at 0, a professor would typically number students starting at 1. Thus, lines 135–136 output student + 1 as the student number to produce grade labels "Student 1: ", "Student 2: ", and so on.

// Fig. 7.14: GradeBook.java
// GradeBook class using an array to store test grades.

public class GradeBook
{
    private String courseName; // name of course this GradeBook represents
    private int[] grades; // array of student grades

    // two-argument constructor initializes courseName and grades array
    public GradeBook( String name, int[] gradesArray )
    {
        courseName = name; // initialize courseName
        grades = gradesArray; // store grades
    } // end two-argument GradeBook constructor

    // method to set the course name
    public void setCourseName( String name )
    {
        courseName = name; // store the course name
    } // end method setCourseName

```
21
22 // method to retrieve the course name
23 public String getCourseName()
24 {
25     return courseName;
26 } // end method getCourseName
27
28 // display a welcome message to the GradeBook user
29 public void displayMessage()
30 {
31     // getCourseName gets the name of the course
32     System.out.printf( "Welcome to the grade book for\n%s!\n\n",
33         getCourseName() );
34 } // end method displayMessage
35
36 // perform various operations on the data
37 public void processGrades()
38 {
39     // output grades array
40     outputGrades();
41
42     // call method getAverage to calculate the average grade
43     System.out.printf( "\nClass average is %.2f\n", getAverage() );
44
45     // call methods getMinimum and getMaximum
46     System.out.printf( "Lowest grade is %d\nHighest grade is %d\n\n",
47         getMinimum(), getMaximum() );
48
49     // call outputBarChart to print grade distribution chart
50     outputBarChart();
51 } // end method processGrades
52
53 // find minimum grade
54 public int getMinimum()
55 {
56     int lowGrade = grades[ 0 ]; // assume grades[ 0 ] is smallest
57
58     // loop through grades array
59     for ( int grade : grades )
60     {
61         // if grade lower than lowGrade, assign it to lowGrade
62         if ( grade < lowGrade )
63             lowGrade = grade; // new lowest grade
64     } // end for
65
66     return lowGrade; // return lowest grade
67 } // end method getMinimum
68
69 // find maximum grade
70 public int getMaximum()
71 {
72     int highGrade = grades[ 0 ]; // assume grades[ 0 ] is largest
```

```
// loop through grades array
for ( int grade : grades )
{
    // if grade greater than highGrade, assign it to highGrade
    if ( grade > highGrade )
        highGrade = grade; // new highest grade
} // end for

return highGrade; // return highest grade
} // end method getMaximum

// determine average grade for test
public double getAverage()
{
    int total = 0; // initialize total

    // sum grades for one student
    for ( int grade : grades )
        total += grade;

    // return average of grades
    return (double) total / grades.length;
} // end method getAverage

// output bar chart displaying grade distribution
public void outputBarChart()
{
    System.out.println( "Grade distribution:" );

    // stores frequency of grades in each range of 10 grades
    int[] frequency = new int[ 11 ];

    // for each grade, increment the appropriate frequency
    for ( int grade : grades )
        ++frequency[ grade / 10 ];

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
```
