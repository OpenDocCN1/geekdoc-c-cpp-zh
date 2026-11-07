acters. If no match occurs, the `default` case executes, and lines 93–94 print an error message indicating that an incorrect letter grade was entered. If no match occurs in a `switch` statement that does not contain a `default` case, program control continues with the first statement after the switch.

![](bbox=[0.16, 0.195, 0.216, 0.239])

> **Error-Prevention Tip 5.3**
> 
> Provide a `default` case in `switch` statements. Cases not explicitly tested in a `switch` statement without a `default` case are ignored. Including a `default` case focuses you on the need to process exceptional conditions. There are situations in which no `default` processing is needed. Although the `case` clauses and the `default` case in a `switch` statement can occur in any order, it’s common practice to place the `default` clause last.

![](bbox=[0.16, 0.319, 0.216, 0.357])

> **Good Programming Practice 5.6**
> 
> The last case in a `switch` statement does not require a `break` statement. Some programmers include this `break` for clarity and for symmetry with other cases.

# Ignoring Newline, Tab and Blank Characters in Input

Lines 87–90 in the `switch` statement of Fig. 5.10 cause the program to skip newline, tab and blank characters. Reading characters one at a time can cause problems. To have the program read the characters, we must send them to the computer by pressing the `Enter` key. This places a newline character in the input after the character we wish to process. Often, this newline character must be specially processed. By including these cases in our `switch` statement, we prevent the error message in the `default` case from being printed each time a newline, tab or space is encountered in the input.

# Testing Class GradeBook

Figure 5.11 creates a GradeBook object (line 8). Line 10 invokes the its `displayMessage` member function to output a welcome message to the user. Line 11 invokes member function object’s `inputGrades` to read a set of grades from the user and keep track of how many students received each grade. The output window in Fig. 5.11 shows an error message displayed in response to entering an invalid grade (i.e., E). Line 12 invokes GradeBook member function `displayGradeReport` (defined in lines 101–111 of Fig. 5.10), which outputs a report based on the grades entered (as in the output in Fig. 5.11).

```
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
```

**Fig. 5.11** | Creating a GradeBook object and calling its member functions. (Part 1 of 2.)