![](bbox=[0.26, 0.08, 0.88, 0.28])

Figure 3.6 Flowchart for if/else statement.

Another example of the if/else statement is the following:

```
if (fabs(denominator) < 0.0001)
    printf("Denominator close to zero");
else
{
    x = numerator/denominator;
    printf("x = %f \\n",x);
}
```

In this example, we examine the absolute value of the variable denominator. If this value is close to zero, we print a message indicating that we cannot perform the division. If the value of denominator is not close to zero, we compute and print the value of x. The flowchart for this statement was shown in Figure 3.3.

Consider the following set of nested if/else statements:

```
if (x > y)
    if (y < z)
        k++;
    else
        m++;
else
    j++;
```

The value of k is incremented when x > y and y < z. The value of m is incremented when x > y and y >= z. The value of j is incremented when x <= y. With careful indenting, this statement is easy to follow. Suppose that we now eliminate the else portion of the inner if statement. If we keep the same indentation, the statements become the following:

```
if (x > y)
    if (y < z)
        k++;
else
    j++;
```