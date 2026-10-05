# The syntax of the for statement

```
for (initializationExpression; booleanExpression; incrementExpression)
{
    statements
}
```

# A loop that stores the numbers 0 through 4 in a string

With a single statement

```
string numbers = null;
for (int i = 0; i < 5; i++)
numbers += i + " ";
```

With a block of statements

```
string numbers = null;
for (int i = 0; i < 5; i++)
{
    numbers += i;
    numbers += i + " ";
}
```

# A loop that adds the numbers 8, 6, 4, and 2

```
int sum = 0;
for (int j = 8; j > 0; j-=2)
{
    sum += j;
}
```

# A loop that calculates a future value

```
for (int i = 1; i <= months; i++)
{
    futureValue = (futureValue + monthlyPayment) * 
    (1 + monthlyInterestRate);
}
```

# Description

+   * The for statement is useful when you need to increment or decrement a counter that determines how many times the for loop is executed.
* Within the parents of a for loop, you code an initialization expression that declares a counter variable and assigns a starting value to it, a Boolean expression that specifies the condition under which the loop executes, and an increment expression that indicates how the counter variable should be incremented or decremented each time the loop is executed.

![](bbox=[0.056, 0.941, 0.376, 0.957])