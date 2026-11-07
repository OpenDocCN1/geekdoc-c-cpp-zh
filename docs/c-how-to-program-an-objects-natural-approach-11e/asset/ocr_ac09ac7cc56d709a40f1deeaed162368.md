```
1. set total to zero
2. set grade counter to one
3.
4. while grade counter is less than or equal to ten
   5. prompt the user to enter the next grade
   6. input the next grade
   7. add the grade into the total
   8. add one to the grade counter
9.
10. set the class average to the total divided by ten
11. print the class average
```

Note the references in the preceding algorithm to a total and a counter. A total is a variable used to accumulate the sum of several values. A counter is a variable used to count—the grade counter indicates which of the 10 grades is about to be entered by the user. Variables used to store totals must be initialized to zero before being used in a program. In pseudocode, we do not use braces around the statements that form the pseudocode while’s body, but you could.

Experience has shown that the most challenging part of solving a problem on a computer is developing the algorithm for the solution. Once a correct algorithm has been specified, producing a working C++ program from it is usually straightforward.

# 3.8.2 Implementing Counter-Controlled Iteration

In Fig. 3.1, the main function calculates the class average with counter-controlled iteration. It allows the user to enter 10 grades, then calculates and displays the class average.

```
```cpp
// fig03_01.cpp
// Solving the class-average problem using counter-controlled iteration.
#include <iostream>
using namespace std;

int main() {
   // initialization phase
   int total{0}; // initialize sum of grades entered by the user
   int gradeCounter{1}; // initialize grade # to be entered next

   // processing phase uses counter-controlled iteration
   while (gradeCounter <= 10) { // loop 10 times
      cout << "Enter grade: "; // prompt
      int grade;
      cin >> grade; // input next grade
      total = total + grade; // add grade to total
      gradeCounter = gradeCounter + 1; // increment counter by 1
   }
}
```
```

**Fig. 3.1** | Solving the class-average problem using counter-controlled iteration. (Part 1 of 2.)