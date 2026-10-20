# A loop with a break statement

```
string message = null;
int i = 1;
while (i <= months)
{
    futureValue = (futureValue + monthlyPayment) *
        (1 + monthlyInterestRate);
    if (futureValue > 100000)
    {
        message = "Future value is too large.";
        break;
    }
    i++;
}
```

# A loop with a continue statement

```
string numbers = null;
for (int i = 1; i < 6; i++)
{
    numbers += i;
    numbers += "\n";
    if (i < 4)
        continue;
    numbers += "Big\n";
}
```

# The result of the previous loop

```
1
2
3
4
Big
5
Big
```

# Description

+   - You use a break statement to jump out of a loop.
+   - You use a continue statement to jump to the start of a loop.