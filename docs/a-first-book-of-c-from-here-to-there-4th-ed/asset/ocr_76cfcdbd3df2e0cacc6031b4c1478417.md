# EXERCISES 4.4

```
1. switch (letterGrade)
{
    case 'A':
        cout << "The numerical grade is between 90 and 100";
        break;
    case 'B':
        cout << "The numerical grade is between 80 and 89.9";
        break;
    case 'C':
        cout << "The numerical grade is between 70 and 79.9";
        break;
    case 'D':
        cout << "How are you going to explain this one?";
        break;
    default:
        cout << "Of course I had nothing to do with the grade.";
        cout << "\nIt must have been the professor's fault.";
}
```

7. The expression in the switch statement must evaluate to an integer quantity and be tested for equality. The if-else chain in Program 4.5 compares double-precision values, violating the switch statement's requirements for integer relational expressions.

# Chapter 5

# EXERCISES 5.1

+   3. a. 21 numbers are displayed, with 1 being the first and 21 being the last.
+      b. See solution file pgm5-1ex3.cpp.
+      c. 21 numbers would still be printed, but the first number would be 0 and the last would be 20.

# EXERCISES 5.2

+   5. a. Yes, the program yields the correct results because the last time through the loop, it takes the average of the final total.
+      b. Having the average calculate outside the loop is better because the program does the calculation once instead of each time the loop executes.