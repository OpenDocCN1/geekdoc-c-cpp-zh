Line 49 indicates that the while statement should continue looping (also called iter-\nating) as long as gradeCounter’s value is less than or equal to 10. While this condition\nremains true, the while statement repeatedly executes the statements between the braces\nthat delimit its body (lines 49–50).

Line 51 displays the prompt "Enter grade: ". This line corresponds to the pseudo-\ncode statement “Prompt the user to enter the next grade.” Line 53 reads the grade entered by\nthe user and assigns it to variable grade. This line corresponds to the pseudocode state-\nment “Input the next grade.” Line 54 adds the new grade entered by the user to the total\nand assigns the result to total, which replaces its previous value.

Line 55 adds 1 to gradeCounter to indicate that the program has processed the cur-\nrent grade and is ready to input the next grade from the user. Incrementing gradeCounter\neventually causes gradeCounter to exceed 10. At that point the while loop terminates\nbecause its condition (line 49) becomes false.

When the loop terminates, line 59 performs the averaging calculation and assigns its\nresult to the variable average. Line 62 displays the text "Total of all 10 grades is "\nfollowed by variable total’s value. Line 63 then displays the text "Class average is "\nfollowed by variable average’s value. Member function determineClassAverage then\nreturns control to the calling function (i.e., main in Fig. 4.10).

# Demonstrating Class GradeBook

Figure 4.10 contains this application’s main function, which creates an object of class\nGradeBook and demonstrates its capabilities. Line 9 of Fig. 4.10 creates a new GradeBook\nobject called myGradeBook. The string in line 9 is passed to the GradeBook constructor\n(lines 9–12 of Fig. 4.9). Line 11 of Fig. 4.10 calls myGradeBook’s displayMessage mem-\nber function to display a welcome message to the user. Line 12 then calls myGradeBook’s\ndetermineClassAverage member function to allow the user to enter 10 grades, for which\nthe member function then calculates and prints the average—the member function per-\nforms the algorithm shown in the pseudocode of Fig. 4.7.

```
```cpp
// Fig. 4.10: fig04_10.cpp
// Create GradeBook object and invoke its determineClassAverage function.
#include "GradeBook.h" // include definition of class GradeBook

int main()
{
   // create GradeBook object myGradeBook and
   // pass course name to constructor
   GradeBook myGradeBook( "CS101 C++ Programming" );

   myGradeBook.displayMessage(); // display welcome message
   myGradeBook.determineClassAverage(); // find average of 10 grades
} // end main
```
```

![](bbox=[0.086, 0.837, 0.918, 0.895])

**Fig. 4.10** Class average problem using counter-controlled repetition: Creating a GradeBook\nobject (Fig. 4.8–Fig. 4.9) and invoking its determineClassAverage member function. (Part 2 of 2.)