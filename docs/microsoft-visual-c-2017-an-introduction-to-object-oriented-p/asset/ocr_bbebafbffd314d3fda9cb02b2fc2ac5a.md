# Using Compound Expressions in if Statements

```
// using the || operator
if(age < 0 || age > 120)
    WriteLine("Age is not valid");

// using nested ifs
if(age < 0)
    WriteLine("Age is not valid");
else
    if(age > 120)
        WriteLine("Age is not valid");
```

**Figure 4-15** Comparison of the || operator and nested ifs

When the || operator is used in an if statement, any one of the two Boolean expressions the tested expression needs to be true for the resulting action to occur. When the first Boolean expression is true, the second expression is never evaluated because it doesn't matter whether the second expression is true or false. As with the && operator, this feature is called short-circuit evaluation.

+   * Watch the video Using the AND and OR Operators.

# Using the Logical AND and OR Operators

C# provides two logical operators that you generally do not want to use when making comparisons. However, you should learn about them because they might be used in programs written by others, and you might use one by mistake when you intend to use a conditional operator.
The Logical AND operator (&) and Boolean logical OR operator (|) work just like their && (conditional AND) and OR counterparts, they do not support short-circuit evaluation. That is, always evaluate both sides of the expression, no matter what the first evaluation is. This can lead to a side effect, or unintended consequence. For example, in the statement that uses &&, if salesAmountForYear is not least 10,000, the first half of the expression is false, the second half of the Boolean expression is never evaluated and yearsOfService is not increased.

```
if(salesAmountForYear >= 10000 && ++yearsOfService > 10)
    bonus = 20;
```

On the other hand, when a single | is used and salesAmountForYear is not least 10,000, even though the first half of the expression is false, and bonus is not set to 200, the second half of the expression is still evaluated, and yearsOfService is always increased whether it is more than 10 or not:

```
if(salesAmountForYear >= 10000 && ++yearsOfService > 10)
    bonus = 200;
```