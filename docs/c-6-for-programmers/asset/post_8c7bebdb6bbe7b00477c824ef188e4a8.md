
## Applications of Floating-Point Numbers

Floating-point numbers have numerous applications, especially for measured values. For example, when we speak of a "normal" body temperature of 98.6 degrees Fahrenheit, we need not be precise to a large number of digits. When we read the temperature on a thermometer as 98.6, it may actually be 98.5999473210643. Calling this number simply 98.6 is fine for most applications involving body temperatures. Similarly, we used type double to perform class-average calculations in Chapter 5. Due to the imprecise nature of floating-point numbers, type double is preferred over type float, because double variables can represent floating-point numbers more precisely. For this reason, we use type double throughout the book, unless we're manipulating monetary amounts, in which case we use decimal.

## 6.6 do...while Iteration Statement

The do...while iteration statement is similar to the while statement. In the while, the app tests the loop-continuation condition at the beginning of the loop, before executing the loop's body. If the condition is false, the body never executes. The do...while statement tests the loop-continuation condition after executing the loop's body; therefore, the body always executes at least once. When a do...while statement terminates, execution continues with the next statement in sequence. Figure 6.7 uses a do...while (lines 11–15) to output the numbers 1–10.

```csharp
// Fig. 6.7: DoWhileTest.cs
// do...while iteration statement.
using System;

class DoWhileTest
{
   static void Main()
   {
      int counter = 1; // initialize counter

      do
      {
         Console.Write( $"{counter} " );
         ++counter;
      } while ( counter <= 10 ); // required semicolon

      Console.WriteLine();
   }
}
```

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|

Fig. 6.7 | do...while iteration statement.

Line 9 declares and initializes control variable counter. Upon entering the do...while statement, line 13 outputs counter's value, and line 14 increments counter. Then the app evaluates the loop-continuation test at the bottom of the loop (line 15). If the condition is true, the loop continues from the first body statement (line 13). If the condition is false, the loop terminates, and the app continues with the next statement after the loop (line 17).

### UML Activity Diagram for the do...while Iteration Statement

Figure 6.8 contains the UML activity diagram for the do...while statement. This diagram makes it clear that the loop-continuation condition is not evaluated until after the loop performs the action state at least once. Compare this activity diagram with that of the while statement (Fig. 5.6).

![](img/3f5ef6be1748bb746e5f71a483bba4d0_168_0.png)

**Fig. 6.8** | do...while iteration statement UML activity diagram.

## 6.7 switch Multiple-Selection Statement

We discussed the if and if...else selection statements in Chapter 5. C# provides the switch multiple-selection statement to perform different actions based on the possible values of an expression, known as the switch expression. Each action is associated with one or more of the switch expression's possible values. These are specified as constant integral expressions or constant string expressions:

- A constant integral expression is any expression involving character and integer constants that evaluates to an integer value—i.e., values of type sbyte, byte, short, ushort, int, uint, long, ulong and char, or a constant from an enum type (enum is discussed in Section 7.9).
- A constant string expression is any expression composed of string literals or constant string variables that always results in the same string.

### 6.7.1 Using a switch Statement to Count A, B, C, D and F Grades

Figure 6.9 calculates the class average of a set of numeric grades entered by the user, and uses a switch statement to determine whether each grade is the equivalent of an A, B, C, D or F and to increment the appropriate grade counter. The program also displays a summary of the number of students who received each grade.

```csharp
// Fig. 6.9: LetterGrades.cs
// Using a switch statement to count letter grades.
using System;

class LetterGrades
{
    static void Main()
    {
        int total = 0; // sum of grades
        int gradeCounter = 0; // number of grades entered
        int aCount = 0; // count of A grades
        int bCount = 0; // count of B grades
        int cCount = 0; // count of C grades
        int dCount = 0; // count of D grades
        int fCount = 0; // count of F grades

        Console.WriteLine("Enter the integer grades in the range 0-100.");
        Console.WriteLine(
            "Type <Ctrl> z and press Enter to terminate input:");

        string input = Console.ReadLine(); // read user input

        // Loop until user enters the end-of-file indicator (<Ctrl> z)
        while (input != null)
        {
            int grade = int.Parse(input); // read grade off user input
            total += grade; // add grade to total
            ++gradeCounter; // increment number of grades

            // determine which grade was entered
            switch (grade / 10)
            {
                case 9: // grade was in the 90s
                case 10: // grade was 100
                    ++aCount; // increment aCount
                    break; // necessary to exit switch
                case 8: // grade was between 80 and 89
                    ++bCount; // increment bCount
                    break; // exit switch
                case 7: // grade was between 70 and 79
                    ++cCount; // increment cCount
                    break; // exit switch
                case 6: // grade was between 60 and 69
                    ++dCount; // increment dCount
                    break; // exit switch
                default: // grade was less than 60
                    ++fCount; // increment fCount
                    break; // exit switch
            }

            input = Console.ReadLine(); // read user input
        }

        Console.WriteLine("\nGrade Report:");

        // if user entered at least one grade...
        if (gradeCounter != 0)
        {
            // calculate average of all grades entered
            double average = (double) total / gradeCounter;

            // output summary of results
            Console.WriteLine(
                $"Total of the {gradeCounter} grades entered is {total}");
            Console.WriteLine($"Class average is {average:F}");
            Console.WriteLine("Number of students who received each grade:");
            Console.WriteLine($"A: {aCount}"); // display number of A grades
            Console.WriteLine($"B: {bCount}"); // display number of B grades
            Console.WriteLine($"C: {cCount}"); // display number of C grades
            Console.WriteLine($"D: {dCount}"); // display number of D grades
            Console.WriteLine($"F: {fCount}"); // display number of F grades
        }
        else // no grades were entered, so output appropriate message
        {
            Console.WriteLine("No grades were entered");
        }
    }
}
```

```text
Enter the integer grades in the range 0-100.
Type <Ctrl> z and press Enter to terminate input:
99
92
45
57
63
71
76
85
90
100
^Z

Grade Report:
Total of the 10 grades entered is 778
Class average is 77.80
Number of students who received each grade:
A: 4
B: 1
C: 2
D: 1
F: 2
```

Fig. 6.9 | Using a switch statement to count letter grades. (Part 2 of 2.)

Lines 9 and 10 declare and initialize to 0 local variables total and gradeCounter to keep track of the sum of the grades entered by the user and the number of grades entered, respectively. Lines 11–15 declare and initialize to 0 counter variables for each grade category. The main method has two key parts. Lines 21–52 read an arbitrary number of integer grades from the user using sentinel-controlled iteration, update variables total and gradeCounter, and increment an appropriate letter-grade counter for each grade entered. Lines 54–76 output a report containing the total of all grades entered, the average grade and the number of students who received each letter grade.

### Reading Grades from the User

Lines 17–19 prompt the user to enter integer grades and to type Ctrl + z, then press Enter to terminate the input. The notation Ctrl + z means to hold down the Ctrl key and tap the z key when typing in a Command Prompt. Ctrl + z is the Windows key sequence for typing the end-of-file indicator. This is one way to inform an app that there’s no more data to input. If Ctrl + z is entered while the app is awaiting input with a ReadLine method, null is returned. (The end-of-file indicator is a system-dependent keystroke combination. On many non-Windows systems, end-of-file is entered by typing Ctrl + d.) In Chapter 17, Files and Streams, we’ll see how the end-of-file indicator is used when an app reads its input from a file. Windows typically displays the characters ^Z in a Command Prompt when the end-of-file indicator is typed, as shown in the program’s output.

Line 21 uses Console's ReadLine method to get the first line that the user entered and store it in variable input. The while statement (lines 24–52) processes this input. The condition at line 24 checks whether the value of input is null—Console's ReadLine method returns null only if the user typed an end-of-file indicator. As long as the end-of-file indicator has not been typed, input will not be null and the condition will pass. Line 26 converts the string in input to an int type. Line 27 adds grade to total. Line 28 increments gradeCounter.

### Processing the Grades

The switch statement (lines 31–49) determines which counter to increment. In this example, we assume that the user enters a valid grade in the range 0–100. A grade in the range 90–100 represents A, 80–89 represents B, 70–79 represents C, 60–69 represents D and 0–59 represents F. The switch statement consists of a block that contains a sequence of case labels and an optional default label. These are used in this example to determine which counter to increment based on the grade.

### The switch Statement

When control reaches the switch statement, the app evaluates the expression grade / 10 in the parentheses—this is the switch expression. The app attempts to match the value of the switch expression with one of the case labels. The switch expression in line 31 performs integer division, which truncates the fractional part of the result. Thus, when we divide any value in the range 0–100 by 10, the result is always a value from 0 to 10. We use several of these values in our case labels. For example, if the user enters the integer 85, the switch expression evaluates to int value 8. If a match occurs between the switch expression and a case (case 8: at line 37), the app executes the statements for that case. For the integer 8, line 38 increments bCount, because a grade in the 80s is a B. The break statement (line 39) causes program control to proceed with the first statement after the switch (line 51), which reads the next line entered by the user and assigns it to the variable input. Line 52 marks the end of the body of the while statement that
