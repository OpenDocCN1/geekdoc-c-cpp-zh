
In Fig. 4.5 and Fig. 4.8, we included blank lines and indentation in the pseudocode to make it more readable. The blank lines separate the algorithms into their phases and set off control statements; the indentation emphasizes the bodies of the control statements.

The pseudocode algorithm in Fig. 4.8 solves the more general class-average problem. This algorithm was developed after two refinements. Sometimes more are needed.

## Software Engineering Observation 4.4

Terminate the top-down, stepwise refinement process when you’ve specified the pseudocode algorithm in sufficient detail for you to convert the pseudocode to Java. Normally, implementing the Java program is then straightforward.

## Software Engineering Observation 4.5

Some programmers do not use program development tools like pseudocode. They feel that their ultimate goal is to solve the problem on a computer and that writing pseudocode merely delays the production of final outputs. Although this may work for simple and familiar problems, it can lead to serious errors and delays in large, complex projects.

## Implementing Sentinel-Controlled Repetition in Class GradeBook

Figure 4.9 shows the Java class GradeBook containing method determineClassAverage that implements the pseudocode algorithm of Fig. 4.8. Although each grade is an integer, the averaging calculation is likely to produce a number with a decimal point—in other words, a real (i.e., floating-point) number. The type int cannot represent such a number, so this class uses type double to do so.

```
// Fig. 4.9: GradeBook.java
// GradeBook class that solves the class-average problem using
// sentinel-controlled repetition.
import java.util.Scanner; // program uses class Scanner

public class GradeBook
{
    private String courseName; // name of course this GradeBook represents

    // constructor initializes courseName
    public GradeBook( String name )
    {
        courseName = name; // initializes courseName
    } // end constructor

    // method to set the course name
    public void setCourseName( String name )
    {
        courseName = name; // store the course name
    } // end method setCourseName

    // method to retrieve the course name
    public String getCourseName()
{
```

Fig. 4.9 | GradeBook class that solves the class-average problem using sentinel-controlled repetition. (Part 1 of 3.)

```
    return courseName;
} // end method getCourseName

// display a welcome message to the GradeBook user
public void displayMessage()
{
    // getCourseName gets the name of the course
    System.out.printf( "Welcome to the grade book for\n%s!\n\n",
        getCourseName() );
} // end method displayMessage

// determine the average of an arbitrary number of grades
public void determineClassAverage()
{
    // create Scanner to obtain input from command window
    Scanner input = new Scanner( System.in );

    int total; // sum of grades
    int gradeCounter; // number of grades entered
    int grade; // grade value
    double average; // number with decimal point for average

    // initialization phase
    total = 0; // initialize total
    gradeCounter = 0; // initialize loop counter

    // processing phase
    // prompt for input and read grade from user
    System.out.print( "Enter grade or -1 to quit: " );
    grade = input.nextInt();

    // loop until sentinel value read from user
    while ( grade != -1 )
    {
        total = total + grade; // add grade to total
        gradeCounter = gradeCounter + 1; // increment counter

        // prompt for input and read next grade from user
        System.out.print( "Enter grade or -1 to quit: " );
        grade = input.nextInt();
    } // end while

    // termination phase
    // if user entered at least one grade...
    if ( gradeCounter != 0 )
    {
        // calculate average of all grades entered
        average = (double) total / gradeCounter;

        // display total and average (with two digits of precision)
        System.out.printf( "\nTotal of the %d grades entered is %d\n",
            gradeCounter, total );
```

Fig. 4.9 | GradeBook class that solves the class-average problem using sentinel-controlled repetition. (Part 2 of 3.)

```
77        System.out.printf( "Class average is %.2f\n", average );
78    } // end if
79    else // no grades were entered, so output appropriate message
80        System.out.println( "No grades were entered" );
81    } // end method determineClassAverage
82 } // end class GradeBook
```

Fig. 4.9 | GradeBook class that solves the class-average problem using sentinel-controlled repetition. (Part 3 of 3.)

In this example, we see that control statements may be stacked on top of one another (in sequence). The while statement (lines 57–65) is followed in sequence by an if...else statement (lines 69–80). Much of the code in this program is identical to that in Fig. 4.6, so we concentrate on the new concepts.

Line 45 declares double variable average, which allows us to store the class average as a floating-point number. Line 49 initializes gradeCounter to 0, because no grades have been entered yet. Remember that this program uses sentinel-controlled repetition to input the grades. To keep an accurate record of the number of grades entered, the program increments gradeCounter only when the user enters a valid grade.

## Program Logic for Sentinel-Controlled Repetition vs. Counter-Controlled Repetition

Compare the program logic for sentinel-controlled repetition in this application with that for counter-controlled repetition in Fig. 4.6. In counter-controlled repetition, each iteration of the while statement (e.g., lines 52–58 of Fig. 4.6) reads a value from the user, for the specified number of iterations. In sentinel-controlled repetition, the program reads the first value (lines 53–54 of Fig. 4.9) before reaching the while. This value determines whether the program’s flow of control should enter the body of the while. If the condition of the while is false, the user entered the sentinel value, so the body of the while does not execute (i.e., no grades were entered). If, on the other hand, the condition is true, the body begins execution, and the loop adds the grade value to the total (line 59). Then lines 63–64 in the loop body input the next value from the user. Next, program control reaches the closing right brace of the loop body at line 65, so execution continues with the test of the while’s condition (line 57). The condition uses the most recent grade input by the user to determine whether the loop body should execute again. The value of variable grade is always input from the user immediately before the program tests the while condition. This allows the program to determine whether the value just input is the sentinel value before the program processes that value (i.e., adds it to the total). If the sentinel value is input, the loop terminates, and the program does not add –1 to the total.

> Good Programming Practice 4.3
> In a sentinel-controlled loop, prompts should remind the user of the sentinel.

After the loop terminates, the if...else statement at lines 69–80 executes. The condition at line 69 determines whether any grades were input. If none were input, the else part (lines 79–80) of the if...else statement executes and displays the message "No grades were entered" and the method returns control to the calling method.

Notice the while statement’s block in Fig. 4.9 (lines 58–65). Without the braces, the loop would consider its body to be only the first statement, which adds the grade to the total. The last three statements in the block would fall outside the loop body, causing the computer to interpret the code incorrectly as follows:

```
while ( grade != -1 )
    total = total + grade; // add grade to total
    gradeCounter = gradeCounter + 1; // increment counter
    // prompt for input and read next grade from user
    System.out.print( "Enter grade or -1 to quit: " );
    grade = input.nextInt();
```

The preceding code would cause an infinite loop in the program if the user did not input the sentinel -1 at line 54 (before the while statement).

## Common Programming Error 4.5

> Omitting the braces that delimit a block can lead to logic errors, such as infinite loops. To prevent this problem, some programmers enclose the body of every control statement in braces, even if the body contains only a single statement.

## Explicitly and Implicitly Converting Between Primitive Types

If at least one grade was entered, line 72 of Fig. 4.9 calculates the average of the grades. Recall from Fig. 4.6 that integer division yields an integer result. Even though variable average is declared as a double (line 45), the calculation

```
average = total / gradeCounter;
```

loses the fractional part of the quotient before the result of the division is assigned to average. This occurs because total and gradeCounter are both integers, and integer division yields an integer result. To perform a floating-point calculation with integer values, we must temporarily treat these values as floating-point numbers for use in the calculation. Java provides the unary cast operator to accomplish this task. Line 72 uses the (double) cast operator—a unary operator—to create a temporary floating-point copy of its operand total (which appears to the right of the operator). Using a cast operator in this manner is called explicit conversion or type casting. The value stored in total is still an integer.

The calculation now consists of a floating-point value (the temporary double version of total) divided by the integer gradeCounter. Java knows how to evaluate only arithmetic expressions in which the operands’ types are identical. To ensure that the operands are of the same type, Java performs an operation called promotion (or implicit conversion) on selected operands. For example, in an expression containing values of the types int and double, the int values are promoted to double values for use in the expression. In this example, the value of gradeCounter is promoted to type double, then the floating-point division is performed and the result of the calculation is assigned to average. As long as the (double) cast operator is applied to any variable in the calculation, the calculation will yield a double result. Later in this chapter, we discuss all the primitive types. You’ll learn more about the promotion rules in Section 6.7.

## Common Programming Error 4.6

> A cast operator can be used to convert between primitive numeric types, such as int and double, and between related reference types (as we discuss in Chapter 10, Object-Oriented Programming: Polymorphism). Casting to the wrong type may cause compilation errors or runtime errors.
