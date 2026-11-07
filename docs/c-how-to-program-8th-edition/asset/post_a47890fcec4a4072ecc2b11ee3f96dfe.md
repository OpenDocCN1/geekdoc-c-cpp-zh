
> **Portability Tip 5.2**
>
> Testing the symbolic constant `EOF` rather than −1 makes programs more portable. The ANSI/ISO C standard, from which C++ adopts the definition of `EOF`, states that `EOF` is a negative integral value, so `EOF` could have different values on different systems.

In this program, the user enters grades at the keyboard. When the user presses the Enter (or the Return) key, the characters are read by the `cin.get()` function, one character at a time. If the character entered is not end-of-file, the flow of control enters the `switch` statement (lines 60–96), which increments the appropriate letter-grade counter.

## switch Statement Details

The `switch` statement consists of a series of **case labels** and an optional **default case**. These are used in this example to determine which counter to increment, based on a grade. When the flow of control reaches the switch, the program evaluates the expression in the parentheses (i.e., grade) following keyword `switch` (line 60). This is called the **controlling expression**. The switch statement compares the value of the controlling expression with each case label. Assume the user enters the letter C as a grade. The program compares C to each case in the switch. If a match occurs (`case 'C':` in line 72), the program executes the statements for that case. For the case C, line 74 increments `cCount` by 1. The `break` statement (line 75) causes program control to proceed with the first statement after the `switch`—in this program, control transfers to line 97. This line marks the end of the body of the `while` loop that inputs grades (lines 57–97), so control flows to the `while`’s condition (line 57) to determine whether the loop should continue executing.

The cases in our switch explicitly test for the lowercase and uppercase versions of the letters A, B, C, D and F. Note the cases in lines 62–63 that test for the values `'A'` and `'a'` (both of which represent the grade A). Listing cases consecutively with no statements between them enables the cases to perform the same set of statements—when the controlling expression evaluates to either `'A'` or `'a'`, the statements in lines 64–65 will execute. Each case can have multiple statements. The switch selection statement does not require braces around multiple statements in each case.

Without break statements, each time a match occurs in the switch, the statements for that case *and* subsequent cases execute until a break statement or the end of the switch is encountered. This feature is perfect for writing a concise program that displays the iterative song “The Twelve Days of Christmas” in Exercise 5.28.

> **Common Programming Error 5.6**
>
> Forgetting a break statement when one is needed in a switch statement is a logic error.

> **Common Programming Error 5.7**
>
> Omitting the space between the word `case` and the integral value tested in a switch statement—e.g., writing `case3` instead of `case 3`—is a logic error. The switch statement will not perform the appropriate actions when the controlling expression has a value of 3.

## Providing a default Case

If no match occurs between the controlling expression’s value and a case label, the `default` case (lines 92–95) executes. We use the default case in this example to process all controlling-expression values that are neither valid grades nor newline, tab or space characters. If no match occurs, the `default` case executes, and lines 93–94 print an error message indicating that an incorrect letter grade was entered. If no match occurs in a `switch` statement that does not contain a `default` case, program control continues with the first statement after the switch.

![](img/bfd978e7e9b192bab46ec2a89e481263_203_0.png)

> **Error-Prevention Tip 5.3**
>
> Provide a `default` case in `switch` statements. Cases not explicitly tested in a `switch` statement without a `default` case are ignored. Including a `default` case focuses you on the need to process exceptional conditions. There are situations in which no `default` processing is needed. Although the `case` clauses and the `default` case in a `switch` statement can occur in any order, it’s common practice to place the `default` clause last.

![](img/bfd978e7e9b192bab46ec2a89e481263_203_1.png)

> **Good Programming Practice 5.6**
>
> The last case in a `switch` statement does not require a `break` statement. Some programmers include this `break` for clarity and for symmetry with other cases.

## Ignoring Newline, Tab and Blank Characters in Input

Lines 87–90 in the `switch` statement of Fig. 5.10 cause the program to skip newline, tab and blank characters. Reading characters one at a time can cause problems. To have the program read the characters, we must send them to the computer by pressing the `Enter` key. This places a newline character in the input after the character we wish to process. Often, this newline character must be specially processed. By including these cases in our `switch` statement, we prevent the error message in the `default` case from being printed each time a newline, tab or space is encountered in the input.

## Testing Class GradeBook

Figure 5.11 creates a GradeBook object (line 8). Line 10 invokes the object’s `displayMessage` member function to output a welcome message to the user. Line 11 invokes the object’s `inputGrades` member function to read a set of grades from the user and keep track of how many students received each grade. The output window in Fig. 5.11 shows an error message displayed in response to entering an invalid grade (i.e., E). Line 12 invokes GradeBook member function `displayGradeReport` (defined in lines 101–111 of Fig. 5.10), which outputs a report based on the grades entered (as in the output in Fig. 5.11).

```cpp
// Fig. 5.11: fig05_11.cpp
// Create GradeBook object, input grades and display grade report.
#include "GradeBook.h" // include definition of class GradeBook

int main()
{
    // create GradeBook object
    GradeBook myGradeBook("CS101 C++ Programming");

    myGradeBook.displayMessage(); // display welcome message
    myGradeBook.inputGrades(); // read grades from user
    myGradeBook.displayGradeReport(); // display report based on grades
} // end main
```

**Fig. 5.11** | Creating a GradeBook object and calling its member functions. (Part 1 of 2.)

![](img/bfd978e7e9b192bab46ec2a89e481263_205_0.png)

**Fig. 5.12** | switch multiple-selection statement UML activity diagram with break statements.

> **Common Programming Error 5.9**
>
> *Providing case labels with identical values in a switch statement is a compilation error.*

In Chapter 13, we present a more elegant way to implement switch logic. We’ll use a technique called polymorphism to create programs that are often clearer, more concise, easier to maintain and easier to extend than programs that use switch logic.

## *Notes on Data Types*

C++ has flexible data type sizes (see Appendix C, Fundamental Types). Different applications, for example, might need integers of different sizes. C++ provides several integer types. The range of integer values for each type depends on the particular computer’s hardware. In addition to the types int and char, C++ provides the types short (an abbreviation of short int) and long (an abbreviation of long int). The minimum range of values for short integers is −32,768 to 32,767. For the vast majority of integer calculations, long integers are sufficient. The minimum range of values for long integers is −2,147,483,648 to 2,147,483,647. On most computers, ints are equivalent either to short or to long. The range of values for an int is at least the same as that for short integers and no larger than that for long integers. The data type char can be used to represent any of the characters in the computer’s character set. It also can be used to represent small integers.
