# Self-Test Exercises

+   5. Does the following sequence produce division by zero?
+   
+   ```cpp
+   j = -1;
+   if ((j > 0) && (1/(j + 1) > 10))
+       cout << i << endl;
+   ```

+   6. Write an `if-else` statement that outputs the word High if the value of the variable `score` is greater than 100 and Low if the value of `score` is at most 100. The variable `score` is of type `int`.

+   7. Suppose savings and expenses are variables of type `double` that have been given values. Write an `if-else` statement that outputs the word Solvent, decreases the value of savings by the value of expenses, and sets the value of expenses to zero provided that savings is at least as large as expenses. If, however, savings is less than expenses, the `if-else` statement simply outputs the word Bankrupt and does not change the value of any variables.

+   8. Write an `if-else` statement that outputs the word Passed provided the value of the variable `exam` is greater than or equal to 60 and also the value of the variable `programsDone` is greater than or equal to 10. Otherwise, the `if-else` statement outputs the word Failed. The variables `exam` and `programsDone` are both of type `int`.

+   9. Write an `if-else` statement that outputs the word Warning provided that either the value of the variable `temperature` is greater than or equal to 100, or the value of the variable `pressure` is greater than or equal to 200, or both. Otherwise, the `if-else` statement outputs the word OK. The variables `temperature` and `pressure` are both of type `int`.

+   10. What is the output of the following? Explain your answers.
+   
+    a.
+   ```cpp
+   if (0)
+       cout << "0 is true";
+   else
+       cout << "0 is false";
+   cout << endl;
+   ```
+   
+    b.
+   ```cpp
+   if (1)
+       cout << "1 is true";
+   else
+       cout << "1 is false";
+   cout << endl;
+   ```
+   
+    c.
+   ```cpp
+   if (-1)
+       cout << "-1 is true";
+   else
+       cout << "-1 is false";
+   cout << endl;
+   ```

> *Note:* This is an exercise only. This is *not* intended to illustrate programming style you should follow.