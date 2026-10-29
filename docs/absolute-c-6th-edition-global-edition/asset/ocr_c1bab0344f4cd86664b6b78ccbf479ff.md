message when you make the mistake of mixing numeric and Boolean operators
in a single expression.

+   2. The expression `2 < x < 3` is legal. However, it does not mean
+      `(2 < x) && (x < 3)`
+      as many would wish. It means `(2 < x) < 3`. Since `(2 < x)` is a Boolean expression, its value is either true or false and is thus converted to either 0 or 1, either of which is less than 3. So, `2 < x < 3` is always true. The result is true regardless of the value of x.
+   
+   3. `(x < -1) || (x > 2)`
+   
+   4. `(x > 1) && (x < 3)`
+   
+   5. No. In the Boolean expression, `(j > 0)` is false (`j` was just assigned `-1`). The `&&` uses short-circuit evaluation, which does not evaluate the second expression if the truth value can be determined from the first expression. The first expression is false, so the second does not matter.

```
if (score > 100)
    cout << "High";
else
    cout << "Low";
```

You may want to add `\n` to the end of the previously quoted strings, depending on the other details of the program.

```
if (savings >= expenses)
{
    savings = savings - expenses;
    expenses = 0;
    cout << "Solvent";
}
else
{
    cout << "Bankrupt";
}
```

You may want to add `\n` to the end of the previously quoted strings, depending on the other details of the program.

```
if ( (exam >= 60) && (programDone >= 10) )
    cout << "Passed";
else
    cout << "Failed";
```

You may want to add `\n` to the end of the previously quoted strings, depending on the other details of the program.

```
if ( (temperature >= 100) || (pressure >= 200) )
    cout << "Warning";
else
    cout << "OK";
```