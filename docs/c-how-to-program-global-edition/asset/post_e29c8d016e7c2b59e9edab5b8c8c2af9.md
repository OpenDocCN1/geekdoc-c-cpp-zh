
## Second Refinement

To proceed to the next level of refinement, i.e., the second refinement, we commit to specific variables. We need a running total of the numbers, a count of how many numbers have been processed, a variable to receive the value of each grade as it's input and a variable to hold the calculated average. The pseudocode statement

*Initialize variables*

may be refined as follows:

- Initialize total to zero
- Initialize counter to zero

Only the total and counter need to be initialized; the variables average and grade (for the calculated average and the user input, respectively) need not be initialized because their values will be calculated and input from the user, respectively. The pseudocode statement

*Input, sum, and count the quiz grades*

requires an iteration structure that successively inputs each grade. Because we do not know in advance how many grades are to be processed, we'll use sentinel-controlled iteration. The user will enter legitimate grades one at a time. After the last legitimate grade is typed, the user will type the sentinel value. The program will test for this value after each grade is input and will terminate the loop when the sentinel is entered. The refinement of the preceding pseudocode statement is then

- Input the first grade (possibly the sentinel)
- While the user has not as yet entered the sentinel
  - Add this grade into the running total
  - Add one to the grade counter
  - Input the next grade (possibly the sentinel)

Notice that in pseudocode, we do not use braces around the set of statements that form the body of the while statement. We simply indent all these statements under the while to show that they all belong to the while. Again, pseudocode is an informal program-development aid.

The pseudocode statement

*Calculate and print the class average*

may be refined as follows:

- If the counter is not equal to zero
  - Set the average to the total divided by the counter
  - Print the average
- else
  - Print "No grades were entered"

Notice that we're being careful here to test for the possibility of division by zero—a fatal error that if undetected would cause the program to fail (often called "crashing"). The complete second refinement is shown in Fig. 3.7.

decimal point. The type int cannot represent such a number. The program introduces the data type float to handle numbers with decimal points (called floating-point numbers) and introduces a special operator called a cast operator to handle the averaging calculation. These features are explained after the program is presented.

// Fig. 3.8: fig03_08.c
// Class-average program with sentinel-controlled iteration.
#include <stdio.h>

// function main begins program execution
int main( void )
{
    unsigned int counter; // number of grades entered
    int grade; // grade value
    int total; // sum of grades

    float average; // number with decimal point for average

    // initialization phase
    total = 0; // initialize total
    counter = 0; // initialize loop counter

    // processing phase
    // get first grade from user
    printf("%s", "Enter grade, -1 to end: "); // prompt for input
    scanf("%d", &grade); // read grade from user

    // loop while sentinel value not yet read from user
    while ( grade != -1 ) {
        total = total + grade; // add grade to total
        counter = counter + 1; // increment counter

        // get next grade from user
        printf("%s", "Enter grade, -1 to end: "); // prompt for input
        scanf("%d", &grade); // read next grade
    } // end while

    // termination phase
    // if user entered at least one grade
    if ( counter != 0 ) {

        // calculate average of all grades entered
        average = ( float ) total / counter; // avoid truncation

        // display average with two digits of precision
        printf("Class average is %.2f", average );
    } // end if
    else { // if no grades were entered, output message
        puts( "No grades were entered" );
    } // end else
} // end function main

Fig. 3.8 | Class-average program with sentinel-controlled iteration. (Part I of 2.)

```
Enter grade, -1 to end: 75
Enter grade, -1 to end: 94
Enter grade, -1 to end: 97
Enter grade, -1 to end: 88
Enter grade, -1 to end: 70
Enter grade, -1 to end: 64
Enter grade, -1 to end: 83
Enter grade, -1 to end: 89
Enter grade, -1 to end: -1
Class average is 82.50
```

```
Enter grade, -1 to end: -1
No grades were entered
```

Fig. 3.8 | Class-average program with sentinel-controlled iteration. (Part 2 of 2.)

Notice the compound statement in the while loop (line 24) in Fig. 3.8. Once again, the braces are necessary to ensure that all four statements are executed within the loop. Without the braces, the last three statements in the body of the loop would fall outside the loop, causing the computer to interpret this code incorrectly as follows:

```
while ( grade != -1 )
    total = total + grade; // add grade to total
    counter = counter + 1; // increment counter
    printf( "%s", "Enter grade, -1 to end: " ); // prompt for input
    scanf( "%d", &grade ); // read next grade
```

This would cause an infinite loop if the user did not input -1 for the first grade.

Error-Prevention Tip 3.5

In a sentinel-controlled loop, explicitly remind the user what the sentinel value is in prompts requesting data entry.

## Converting Between Types Explicitly and Implicitly

Averages do not always evaluate to integer values. Often, an average is a value such as 7.2 or -93.5 that contains a fractional part. These values are referred to as floating-point numbers and can be represented by the data type float. The variable average is defined to be of type float (line 12) to capture the fractional result of our calculation. However, the result of the calculation total / counter is an integer because total and counter are both integer variables. Dividing two integers results in integer division in which any fractional part of the calculation is truncated (i.e., lost). Because the calculation is performed first, the fractional part is lost before the result is assigned to average. To produce a floating-point calculation with integer values, we must create temporary values that are floating-point numbers. C provides the unary cast operator to accomplish this task. Line 38

```
average = ( float ) total / counter;
```

This manner is called explicit conversion. The calculation now consists of a floating-point value (the temporary float version of total) divided by the unsigned int value stored in counter. C evaluates arithmetic expressions only in which the data types of the operands are identical. To ensure that the operands are of the same type, the compiler performs an operation called implicit conversion on selected operands. For example, in an expression containing the data types unsigned int and float, copies of unsigned int operands are made and converted to float. In our example, after a copy of counter is made and converted to float, the calculation is performed and the result of the floating-point division is assigned to average. C provides a set of rules for conversion of operands of different types. We discuss this further in Chapter 5.

Cast operators are available for most data types—they’re formed by placing parentheses around a type name. Each cast operator is a unary operator, i.e., an operator that takes only one operand. In Chapter 2, we studied the binary arithmetic operators. C also supports unary versions of the plus (+) and minus (-) operators, so you can write expressions such as -7 or +5. Cast operators associate from right to left and have the same precedence as other unary operators such as unary + and unary -. This precedence is one level higher than that of the multiplicative operators *, / and %.

### Formatting Floating-Point Numbers

Figure 3.8 uses the printf conversion specifier %.2f (line 41) to print the value of average. The f specifies that a floating-point value will be printed. The .2 is the precision with which the value will be displayed—with 2 digits to the right of the decimal point. If the %f conversion specifier is used (without specifying the precision), the default precision of 6 is used—exactly as if the conversion specifier %.6f had been used. When floating-point values are printed with precision, the printed value is rounded to the indicated number of decimal positions. The value in memory is unaltered. When the following statements are executed, the values 3.45 and 3.4 are printed.

```c
printf( "%.2f\n", 3.446 ); // prints 3.45
printf( "%.1f\n", 3.446 ); // prints 3.4
```

> **Common Programming Error 3.6**
> 
> Using precision in a conversion specification in the format control string of a `scanf` statement is an error. Precisions are used only in `printf` conversion specifications.

### Notes on Floating-Point Numbers

Although floating-point numbers are not always “100% precise,” they have numerous applications. For example, when we speak of a “normal” body temperature of 98.6 Fahrenheit, we do not need to be precise to a large number of digits. When we view the temperature on a thermometer and read it as 98.6, it may actually be 98.5999473210643. The point here is that calling this number simply 98.6 is fine for most applications. We’ll say more about this issue later.

Another way floating-point numbers develop is through division. When we divide 10 by 3, the result is 3.3333333… with the sequence of 3s repeating infinitely. The computer allocates only a fixed amount of space to hold such a value, so the stored floating-point value can be only an approximation.
