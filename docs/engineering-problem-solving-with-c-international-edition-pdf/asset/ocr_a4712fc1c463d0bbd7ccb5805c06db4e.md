![](bbox=[0.22, 0.085, 0.78, 0.315])

# Figure 3.5 Flowchart for if/else statement.

Another example of the if/else statement is

```
if (fabs(denominator) < 0.0001)
    cout << "Denominator close to zero" << endl;
else
{
    x = numerator/denominator;
    cout << "x = " << x << endl;
}
```

In this example, we examine the absolute value of the object denominator. If this value is close to zero, we print a message indicating that we cannot perform the division. If the value of denominator is not close to zero, we compute and print the value of x. The flowchart for this statement was shown in Figure 3.3.

Consider the following set of nested if/else statements:

```
if (x > y)
    if (y < z)
        ++k;
    else
        ++m;
else
    ++j;
```

![](bbox=[0.46, 0.665, 0.86, 0.905])

The value of k is incremented when x>y and y<z. The value of m is incremented when x>y and y>=z. The value of j is incremented when x<=y. With careful indenting, this