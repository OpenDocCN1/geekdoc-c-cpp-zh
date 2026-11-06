
because types `short`, `int` and `long` are guaranteed to be at least as big as type `char`. Thus, we can treat a character either as an integer or as a character, depending on its use. For example, the statement

```cpp
cout << "The character 'a' has the value "
     << static_cast<int>( 'a' ) << endl;
```

prints the character a and its integer value as follows:

```
The character 'a' has the value 97
```

The integer 97 is the character’s numerical representation in the computer. Most computers today use the Unicode character set in which 97 represents the lowercase letter `'a'`. Appendix B shows the characters and decimal equivalents from the ASCII (American Standard Code for Information Interchange) character set, which is a subset of Unicode.

Generally, assignment statements have the value that is assigned to the variable on the left side of the `=`. Thus, the value of the assignment expression `grade = cin.get()` is the same as the value returned by `cin.get()` and assigned to the variable `grade`.

The fact that assignment expressions have values can be useful for assigning the same value to several variables. For example,

```cpp
a = b = c = 0;
```

first evaluates `c = 0` (because the `=` operator associates from right to left). The variable `b` is then assigned the value of `c = 0` (which is 0). Then, `a` is assigned the value of `b (= 0)` (which is also 0). In the program, the value of `grade = cin.get()` is compared with the value of `EOF` (a symbol whose acronym stands for “end-of-file”). We use `EOF` (which normally has the value −1) as the sentinel value. However, you do not type the value −1, nor do you type the letters `EOF` as the sentinel value. Rather, you type a system-dependent keystroke combination that means “end-of-file” to indicate that you have no more data to enter. `EOF` is a symbolic integer constant defined in the `<iostream>` header file. If the value assigned to `grade` is equal to `EOF`, the `while` loop (lines 57–97) terminates. We’ve chosen to represent the characters entered into this program as `ints`, because `EOF` has type `int`.

On UNIX/Linux systems and many others, end-of-file is entered by typing

```
<Ctrl> d
```

on a line by itself. This notation means to press and hold down the Ctrl key, then press the d key. On other systems such as Microsoft Windows, end-of-file can be entered by typing

```
<Ctrl> z
```

> *[Note: In some cases, you must press Enter after the preceding key sequence. Also, the characters ^Z sometimes appear on the screen to represent end-of-file, as shown in Fig. 5.11.]*

![](img/023f159fdd47d944d48e08843cea732d_216_0.png)

## Portability Tip 5.1

> The keystroke combinations for entering end-of-file are system dependent.

![](img/023f159fdd47d944d48e08843cea732d_216_1.png)

## Portability Tip 5.2

> Testing for the symbolic constant `EOF` rather than −1 makes programs more portable. The ANSI/ISO C standard, from which C++ adopts the definition of `EOF`, states that `EOF` is a negative integral value, so `EOF` could have different values on different systems.

In this program, the user enters grades at the keyboard. When the user presses the *Enter* (or *Return*) key, the characters are read by the `cin.get()` function, one character at a time. If the character entered is not end-of-file, the flow of control enters the `switch` statement (lines 60–96), which increments the appropriate letter-grade counter.

## switch Statement Details

The `switch` statement consists of a series of `case` labels and an optional `default` case. These are used in this example to determine which counter to increment, based on a grade. When the flow of control reaches the `switch`, the program evaluates the expression in the parentheses (i.e., `grade`) following keyword `switch` (line 60). This is called the controlling expression. The `switch` statement compares the value of the controlling expression with each `case` label. Assume the user enters the letter C as a grade. The program compares C to each `case` in the `switch`. If a match occurs (`case 'C':` in line 72), the program executes the statements for that case. For the letter C, line 74 increments `cCount` by 1. The `break` statement (line 75) causes program control to proceed with the first statement after the `switch`—in this program, control transfers to line 97. This line marks the end of the body of the `while` loop that inputs grades (lines 57–97), so control flows to the `while`'s condition (line 57) to determine whether the loop should continue executing.

The cases in our `switch` explicitly test for the lowercase and uppercase versions of the letters A, B, C, D and F. Note the cases in lines 62–63 that test for the values `'A'` and `'a'` (both of which represent the grade A). Listing cases consecutively with no statements between them enables the cases to perform the same set of statements—when the controlling expression evaluates to either `'A'` or `'a'`, the statements in lines 64–65 will execute. Each case can have multiple statements. The `switch` selection statement does not require braces around multiple statements in each case.

Without `break` statements, each time a match occurs in the `switch`, the statements for that case and subsequent cases execute until a `break` statement or the end of the `switch` is encountered. This is often referred to as “falling through” to the statements in subsequent cases. (This feature is perfect for writing a concise program that displays the iterative song “The Twelve Days of Christmas” in Exercise 5.28.)

### Common Programming Error 5.8

*Forgetting a `break` statement when one is needed in a `switch` statement is a logic error.*

### Common Programming Error 5.9

*Omitting the space between the word `case` and the integral value being tested in a `switch` statement—e.g., writing `case3:` instead of `case 3:`—is a logic error. The `switch` statement will not perform the appropriate actions when the controlling expression has a value of 3.*

## Providing a `default` Case

If no match occurs between the controlling expression's value and a `case` label, the `default` case (lines 92–95) executes. We use the `default` case in this example to process all controlling-expression values that are neither valid grades nor newline, tab or space characters. If no match occurs, the `default` case executes, and lines 93–94 print an error message indicating that an incorrect letter grade was entered. If no match occurs in a `switch` statement that does not contain a `default` case, program control continues with the first statement after the `switch`.

## Good Programming Practice 5.10

*Provide a `default` case in `switch` statements. Cases not explicitly tested in a `switch` statement without a `default` case are ignored. Including a `default` case focuses you on the need to process exceptional conditions. There are situations in which no `default` processing is needed. Although the `case` clause and the `default` case clause in a `switch` statement can occur in any order, it's common practice to place the `default` clause last.*

## Good Programming Practice 5.11

*The last `case` in the `switch` statement does not require a `break` statement. Some programmers include this `break` for clarity and for symmetry with other cases.*

### Ignoring Newline, Tab and Blank Characters in Input

Lines 87–90 in the `switch` statement of Fig. 5.10 cause the program to skip newline, tab and blank characters. Reading characters one at a time can cause some problems. To have the program read the characters, we must send them to the computer by pressing the Enter key. This places a newline character in the input after the character we wish to process. Often, this newline character must be specially processed. By including the preceding cases in our `switch` statement, we prevent the error message in the `default` case from being printed each time a newline, tab or space is encountered in the input.

### Common Programming Error 5.10

*Not processing newline and other white-space characters in the input when reading characters one at a time can cause logic errors.*

### Testing Class GradeBook

Figure 5.11 creates a `GradeBook` object (line 8). Line 10 invokes its `displayMessage` member function to output a welcome message to the user. Line 11 invokes the object's `inputGrades` member function to read a set of grades from the user and keep track of how many students received each grade. The output window in Fig. 5.11 shows an error message displayed in response to entering an invalid grade (i.e., E). Line 12 invokes `GradeBook` member function `displayGradeReport` (defined in lines 101–111 of Fig. 5.10), which outputs a report based on the grades entered (as in the output in Fig. 5.11).

```cpp
// Fig. 5.11: fig05_11.cpp
// Create GradeBook object, input grades and display grade report.
#include "GradeBook.h" // include definition of class GradeBook

int main()
{
   // create GradeBook object
   GradeBook myGradeBook( "CS101 C++ Programming" );

   myGradeBook.displayMessage(); // display welcome message
```

**Fig. 5.11** | Creating a GradeBook object and calling its member functions. (Part 1 of 2.)
