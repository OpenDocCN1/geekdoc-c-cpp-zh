When more than one statement is used, they are separated by commas and are executed from left to right. This comma operator is executed last in operator precedence.

# PRACTICE!

Determine the number of times that the following for loops are executed.

+   1. for (k=3; k<=20; k++)
+      {
+      statements;
+      }
+   
+   2. for (k=3; k<=20; ++k)
+      {
+      statements;
+      }
+   
+   3. for (count=-2; count<=14; count++)
+      {
+      statements;
+      }
+   
+   4. for (k=2; k>=-10; k--)
+      {
+      statements;
+      }
+   
+   5. for (time=10; time>=5; time++)
+      {
+      statements;
+      }
+   
+   6. What is the value of count after the nested for loops are executed?
+      int k, j, count=0;
+      for (k=-1; k<=3; k++)
+      for (j=3; j>=-1; j--)
+      count++;

# break AND continue STATEMENTS

We used the break statement in a previous section with the switch statement. The break statement can also be used with any of the loop structures presented in this section to immediately exit from the loop in which it is contained. In contrast, the continue statement is used to skip the remaining statements in the current pass, or iteration, of the loop and then continue with the next iteration of the loop. Thus, in a while loop or a do/while loop, the condition is evaluated after the continue statement is executed to determine if the statements in the loop are to be executed again. In a for loop, the loop-control variable is modified, and then the repetition-continuation condition is evaluated to determine whether the statements in the loop are to be executed again. Both the break and continue statements are useful in exiting either the current iteration or the entire loop when error conditions are encountered.