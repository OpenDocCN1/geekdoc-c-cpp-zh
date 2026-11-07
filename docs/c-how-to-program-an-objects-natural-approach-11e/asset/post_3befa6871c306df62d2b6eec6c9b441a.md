
```text
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

Note the references in the preceding algorithm to a total and a counter. A total is a variable used to accumulate the sum of several values. A counter is a variable used to count—the grade counter indicates which of the 10 grades is about to be entered by the user. Variables used to store totals must be initialized to zero before being used in a program. In pseudocode, we do not use braces around the statements that form the pseudocode while's body, but you could.

Experience has shown that the most challenging part of solving a problem on a computer is developing the algorithm for the solution. Once a correct algorithm has been specified, producing a working C++ program from it is usually straightforward.

## 3.8.2 Implementing Counter-Controlled Iteration

In Fig. 3.1, the main function calculates the class average with counter-controlled iteration. It allows the user to enter 10 grades, then calculates and displays the class average.

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
```

**Fig. 3.1** | Solving the class-average problem using counter-controlled iteration. (Part 1 of 2.)

```cpp
   // termination phase
   int average{total / 10}; // int division yields int result

   // display total and average of grades
   cout << "\nTotal of all 10 grades is " << total;
   cout << "\nClass average is " << average << "\n";
}
```

```text
Enter grade: 67
Enter grade: 78
Enter grade: 89
Enter grade: 67
Enter grade: 87
Enter grade: 98
Enter grade: 93
Enter grade: 85
Enter grade: 82
Enter grade: 100

Total of all 10 grades is 846
Class average is 84
```

**Fig. 3.1** | Solving the class-average problem using counter-controlled iteration. (Part 2 of 2.)

### Local Variables in main

Lines 8, 9, 14 and 21 declare int variables total, gradeCounter, grade and average, respectively. Variable grade stores the user input. A variable declared in a block (such as a function's body) is a local variable that can be used only from the line of its declaration to the closing right brace of the block. A local variable's declaration must appear before the variable is used. Variable grade—declared at line 14 in the while loop's body—can be used only in that block.

### Initializing Variables total and gradeCounter

Lines 8–9 declare and initialize total to 0 and gradeCounter to 1. These initializations occur before the variables are used in calculations. Initialize each total and counter, either in its declaration or in an assignment statement. Totals are typically initialized to 0 and counters are typically initialized to 0 or 1, depending on their use. We'll show examples of when to use 0 or 1.

### Reading 10 Grades from the User

The while statement (lines 12–18) continues iterating as long as gradeCounter's value is less than or equal to 10. Line 13 displays the prompt "Enter grade: ". Line 15 inputs the grade entered by the user and assigns it to variable grade. Then line 16 adds the new grade entered by the user to the total and assigns the result to total, replacing its previous value. Line 17 adds 1 to gradeCounter to indicate that the program has processed a grade and is ready to input the next grade from the user. Incrementing gradeCounter eventually causes it to exceed 10, which terminates the loop.

### Calculating and Displaying the Class Average

When the loop terminates, line 21 performs the averaging calculation in the average variable's initializer. Line 24 displays the text "Total of all 10 grades is " followed by variable total's value. Then, line 25 displays the text "Class average is " followed by average's value. When execution reaches line 26, the program terminates.

## 3.8.3 Integer Division and Truncation

This example's average calculation produces an int result. The program's sample execution shows that the sum of the grades is 846—when divided by 10, this should yield 84.6. Numbers like 84.6 containing decimal points are floating-point numbers. However, in the class-average program, total / 10 produces the integer 84 because total and 10 are both integers. Dividing two integers results in integer division—any fractional part of the calculation is truncated. The next section shows how to obtain a floating-point result from the averaging calculation. For example, 7 / 4 yields 1.75 in conventional arithmetic but truncates to 1 in integer arithmetic rather than rounding to 2. Assuming that integer division rounds (rather than truncates) can lead to incorrect results.

## 3.8.4 Arithmetic Overflow

In Fig. 3.1, line 16

```cpp
total = total + grade; // add grade to total
```

adds each grade entered by the user to the total. Even this simple statement has a potential problem—adding the integers could result in a value too large to store in an int variable. This is known as arithmetic overflow and causes undefined behavior, which can lead to unintended results and security problems. See, for example,

```text
https://en.wikipedia.org/wiki/Integer_overflow#Security_ramifications
```

The following expressions return your system's maximum and minimum int values:

```cpp
std::numeric_limits<int>::max()
std::numeric_limits<int>::min()
```

Each uses class numeric_limits from the C++ standard library header `<limits>`. You may use similar expressions for any integral or floating-point type by replacing int in these expressions.

## 3.8.5 Input Validation

When a program receives input from the user, various problems might occur. For example, line 15 of Fig. 3.1

```cpp
cin >> grade; // input next grade
```

assumes that the user will enter an integer grade from 0 to 100 but the user could enter:

- an integer less than 0,
- an integer greater than 100,
- an integer outside the range of values that can be stored in an int variable,
- a number containing a decimal point or
- a value containing letters or special symbols that do not even represent a number.

Industrial-strength programs must test for all possible erroneous cases to ensure valid inputs. A program that inputs grades should validate them using range checking to ensure they are values from 0 to 100. You can then ask the user to re-enter any out-of-range value. If a program requires inputs from a specific set of values (such as, non-sequential product codes), you should ensure that each input matches a value in the set.

### ✔️ Checkpoint

- 1. (True/False) Dividing two integers results in integer division—any fractional part of the calculation is rounded to the nearest integer.
  
  Answer: False. Actually, any fractional part of the calculation is truncated.

- 2. (Fill-in) A variable declared in a(n) _______ (such as a function's body) is a local variable that can be used only from the line of its declaration to the corresponding closing right brace.
  
  Answer: block.

- 3. (Code) Rewrite the initialization in the following code so the loop iterates 5 times.

  ```cpp
  int count{0};

  while (count < 5) {
      count = count + 1;
      cout << "count is: " << count << "\n";
  }
  ```

  Answer:

  ```cpp
  int count{0};

  while (count < 5) {
      count = count + 1;
      cout << "count is: " << count << "\n";
  }
  ```

  ```text
  count is: 1
  count is: 2
  count is: 3
  count is: 4
  count is: 5
  ```

## 3.9 Formulating Algorithms: Sentinel-Controlled Iteration

Let's generalize Section 3.8's class-average problem. Consider the following problem:

> Develop a class-averaging program that processes grades for an arbitrary number of students each time it is run.

In the previous class-average example, the problem statement specified the number of students, so the number of grades (10) was known in advance. For this problem, we do not know how many grades the user will enter during the program's execution. The program must process an arbitrary number of grades.
