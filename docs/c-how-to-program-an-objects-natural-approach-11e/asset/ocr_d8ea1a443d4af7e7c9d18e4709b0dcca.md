```
```cpp
20    // termination phase
21    int average{total / 10}; // int division yields int result
22
23    // display total and average of grades
24    cout << "\nTotal of all 10 grades is " << total;
25    cout << "\nClass average is " << average << "\n";
26 }
```
```

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
```

**Fig. 3.1** | Solving the class-average problem using counter-controlled iteration. (Part 2 of 2.)

# Local Variables in main

Lines 8, 9, 14 and 21 declare int variables total, gradeCounter, grade and average, respectively. Variable grade stores the user input. A variable declared in a block (such as a function’s body) is a local variable that can be used only from the line of its declaration to the closing right brace of the block. A local variable’s declaration must appear before the variable is used. Variable grade—declared at line 14 the while loop’s body—can be used only in that block.

# Initializing Variables total and gradeCounter

Lines 8–9 declare and initialize total to 0 and gradeCounter to 1. These initializations occur before the variables are used in calculations. Initialize each total and counter, either in its declaration or in an assignment statement. Totals are typically initialized to 0 and counters are typically initialized to 0 or 1, depending on their use. We’ll show examples of when to use 0 or 1.

# Reading 10 Grades from the User

The while statement (lines 12–18) continues iterating as long as gradeCounter’s value is less than or equal to 10. Line 13 displays the prompt "Enter grade: ". Line 15 inputs the grade entered by the user and assigns it to variable grade. Then line 16 adds the new grade entered by the user to the total and assigns the result to total, replacing its previous value. Line 17 adds 1 to gradeCounter to indicate that the program has processed a grade and is ready to input the next grade from the user. Incrementing gradeCounter eventually causes it to exceed 10, which terminates the loop.

# Calculating and Displaying the Class Average

When the loop terminates, line 21 performs the averaging calculation in the average variable’s initializer. Line 24 displays the text "Total of all 10 grades is " followed by vari-