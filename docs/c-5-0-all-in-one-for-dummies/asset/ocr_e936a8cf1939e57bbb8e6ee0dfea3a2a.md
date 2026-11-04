If a is greater than b, the first block is executed; otherwise, the second block is executed. In the end, max contains the greater of a or b.

# Avoiding even the else

Sequences of else clauses can become confusing. Some programmers like to avoid them when doing so doesn't cause even more confusion. You could write the maximum calculation like this:

```
// Store the maximum of a and b into the variable max.
int max;
// Start by assuming that a is greater than b.
max = a;
// If it is not . . .
if (b > a)
{
    // . . . then you can change your mind.
    max = b;
}
```

Some programmers avoid this style like the plague, and I can sympathize. (That doesn't mean that I'm going to change; it just means that I sympathize.) You see both this style and the "else" style in common use.

![](bbox=[0.18, 0.58, 0.28, 0.7])

Programmers who like to be cool and cryptic often use the ternary operator, : ?, equivalent to an if/else on one line:

```
bool informal = true;
string name = informal : "Chuck" ? "Charles";  // Returns "Chuck"
```

This chunk evaluates the expression before the colon. If the expression is true, return the value after the colon but before the question mark. If the expression is false, return the value after the question mark. This process turns an if/else into an expression.

I generally advise using ternary only rarely because it truly is cryptic.

# Nesting if statements

The CalculateInterest program warns the user of illegal input; however, continuing with the interest calculation, even if one of the values is illogical, doesn't seem quite right. It causes no real harm here because the interest calculation takes little or no time and the user can ignore the results, but some calculations aren't nearly as quick. In addition, why ask the user for an interest rate after she has already entered an invalid value for the principal? The user knows that the results of the calculation will be invalid no matter what she enters next. (You'd be amazed at how much it infuriates users.)

The program should ask the user for an interest rate only if the principal is reasonable and perform the interest calculation only if both values are valid. To accomplish this, you need two if statements, one within the other.