+   k. false. Since the value of the first subexpression, `(limit < 0)`, is false, you know that the entire expression is false without bothering to evaluate the second subexpression. Thus, the second subexpression,
+   
+   `((limit/count) > 7)`
+   
+   is never evaluated, and so the fact that it involves a division by zero is never noticed by the computer. This is short-circuit evaluation.

+   l. If you think this expression is nonsense, you are correct. The expression has no intuitive meaning, but C++ converts the int values to bool and then evaluates the `&&` and `!` operations. Thus, C++ will evaluate this mess. Recall that in C++, any nonzero integer converts to true and 0 converts to false, so C++ will evaluate
+   
+   `(5 && 7) + (!6)`
+   
+   as follows. In the expression `(5 && 7)`, the 5 and 7 convert to true; `true && true` evaluates to true, which C++ converts to 1. In the expression `(!6)` the 6 is converted to true, so `!` (true) evaluates to false, which C++ converts to 0. Thus, the entire expression evaluates to `1 + 0`, which is 1. The final value is thus 1. C++ will convert the number 1 to true, but the answer has little intuitive meaning as true; it is perhaps better to just say the answer is 1. There is no need to become proficient at evaluating these nonsense expressions, but doing a few will help you to understand why the compiler does not give you an error message when you make the mistake of mixing numeric and Boolean operators in a single expression.

+   2. The expression `2 < x < 3` is legal. However, it does not mean
+   
+   `(2 < x) && (x < 3)`
+   
+   as many would wish. It means `(2 < x) < 3`. Since `(2 < x)` is a Boolean expression, its value is either true or false and is thus converted to either 0 or 1, either of which is less than 3. So, `2 < x < 3` is always true. The result is true regardless of the value of x.

+   3. `(x < −1 || (x > 2)`

+   4. `(x > 1 && (x < 3)`

+   5. No. In the Boolean expression, `(j > 0)` is false (`j` was just assigned −1). The `&&` uses short-circuit evaluation, which does not evaluate the second expression if the truth value can be determined from the first expression. The first expression is false, so the second does not matter.

+   6. If `(score > 100)`
+   
+   ```cpp
+   cout << "High";
+   else
+       cout << "Low";
+   ```
+   
+   You may want to add `\n` to the end of the above quoted strings, depending on the other details of the program.