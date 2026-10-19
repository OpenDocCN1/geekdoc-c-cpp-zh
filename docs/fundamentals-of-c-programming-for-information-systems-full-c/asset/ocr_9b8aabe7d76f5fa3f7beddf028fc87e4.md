The following program shows the modified if statement to implement the new decision structure:

```
bool freeTopping;
if ((subTotal >= 10) || (scoops >=3))
{
    discountPercent = 20;        // processed if either (subTotal >= 10) or (scoops >=3),
    freeTopping = true;          // that is, if one of the two Boolean expressions is true.
}
else
{
    discountPercent = 0;   // processed if both Boolean expressions are not true
    freeTopping = false; // that is, if both are false.
}
```

Step 1-6: Modify the if statement to include the revised criteria. Run and test the form with different combinations of subtotal and scoops so that (1) both Boolean expressions are false, (2) only the first expression is true, (3) only the second expression is true and (4) both expressions are true. Observe the result in each case.

Change the logical operator from "||" (Or) to "&&" (And), run the form and observe the difference under the four different combinations of subtotal and scoops. Change the logical operator back to "||"

The expression ((subTotal >= 10) || (scoops >=3)) checks whether subtotal is at least 10 or scoops is at least 3. An alternative to do the same thing is to check whether the expression ((subTotal < 10) and (scoops < 3)) is false—that is, both subtotal and scoops are not below the required limit. Note that the expressions have the "<" operator in place of ">=". Further, "Or" is replaced by "And."

You can use the "!" (Not) operator to check whether the expression is false, as follows:

```
if (!((subTotal < 10) && (scoops < 3)))
```

Step 1-7: Change the if statement to: if (!((subTotal < 10) && (scoops<3))). Run the form and observe the difference under the four different combinations of subtotal and scoops specified in Step 1-6. Observe the result in each case. Now, change "&&" to "||" as follows:

```
bool freeTopping;
if (!((subTotal < 10) || (scoops < 3)))
{
    discountPercent = 20;
    freeTopping = true;
}
else
{
    discountPercent = 0;
    freeTopping = false;
}
```