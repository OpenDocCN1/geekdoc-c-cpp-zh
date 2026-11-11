The more general conditional in Java looks like this (see [Figure 3.8]):

```
if (condition) statement₁ else statement₂
```

For example:

```
if (yourSales >= target)
{
    performance = "Satisfactory";
    bonus = 100 + 0.01 * (yourSales - target);
}
```