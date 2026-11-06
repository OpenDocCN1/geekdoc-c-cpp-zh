When you define a variable *inside* the loop body, the variable is created for each iteration of the loop and removed after the end of each iteration. For example, consider the interest variable in this loop:

```
```cpp
while (balance < TARGET)
{
    year++;
    double interest = balance * RATE / 100;
    balance = balance + interest;
} // interest no longer defined here
```
```

![](bbox=[0.604, 0.145, 0.833, 0.193])

In contrast, the balance and years variables were defined *outside* the loop body. That way, the same variable is used for all iterations of the loop.

**Figure 2**
Execution of the doubly nested loop

![](bbox=[0.246, 0.283, 0.871, 0.922])

**1. Check the loop condition**

balance = 10000

year = 0

```
```cpp
while (balance < TARGET)
{
    year++;
    double interest = balance * RATE / 100;
    balance = balance + interest;
}
```
```

Callout: “The condition is true.”

**2. Execute the statements in the loop**

balance = 10500

year = 1

interest = 500

```
```cpp
while (balance < TARGET)
{
    year++;
    double interest = balance * RATE / 100;
    balance = balance + interest;
}
```
```

**3. Check the loop condition again**

balance = 10500

year = 1

```
```cpp
while (balance < TARGET)
{
    year++;
    double interest = balance * RATE / 100;
    balance = balance + interest;
}
```
```

Callout: “The condition is still true.”

**4. After 15 iterations**

balance = 20789.28

year = 15

```
```cpp
while (balance < TARGET)
{
    year++;
    double interest = balance * RATE / 100;
    balance = balance + interest;
}
```
```

Callout: “The condition is no longer true.”

**5. Execute the statement following the loop**

balance = 20789.28

year = 15

```
```cpp
while (balance < TARGET)
{
    year++;
    double interest = balance * RATE / 100;
    balance = balance + interest;
}
cout << year << endl;
```
```