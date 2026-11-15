+   3. Put the braces surrounding a block of statements on lines by themselves; this will help you avoid omitting them.
+   4. Do not use the equality operator with floating-point values; instead, test for values "close to" a desired value.
+   5. Recompile your program frequently when correcting syntax errors; correcting one error may remove many error messages.
+   6. Use cout statements to give memory snapshots of the values of key objects when debugging loops. Remember to use the endl manipulator instead of '\n' to ensure that the values are printed immediately after the statement is executed.

# Problems

# Exam Practice!

# True/False Problems

Indicate whether the following statements are true (T) or false (F).

+   1. Relational operators have lower precedence than the assignment operator. T F
+   2. Relational expressions are Boolean expressions, i.e., their value can be either true or false. T F
+   3. Logical operators either join two or more relational expressions or reverse the logic of an expression. T F
+   4. Operators could also be overloaded for built-in data types. T F
+   5. The keyword else is always associated with the closest if statement unless braces are used to define blocks of statements. T F

# Syntax Problems

Identify any syntax errors in the following statements. Assume that the objects have all been defined as integers.

```
6. switch (score)
   {
      case (score < 60):
         cout << "Too low. \n";
         break;
      case (score < 80):
         cout << "You can do better. \n";
         break;
      case score >= 80 && score <= 100):
         cout << "Good Score. Congratulations\n";
         break;
   }
```

# Multiple-Choice Problems

Circle the letter for the best answer to complete each statement or for the correct answer to each question.

+   7. Consider the following statement:
+      int x = 9, y = 15;
+      What does the statement cout << (x == y); display?
+      (a) 1
+      (b) 0
+      (c) 9
+      (d) 15