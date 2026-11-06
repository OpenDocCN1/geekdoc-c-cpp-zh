```
Here is our complete loop:
Read first value; store as highest value.
highest_month = 1
for (current_month = 2; current_month <= 12; current_month++)
    Read next value.
    If value is higher than the highest value, set highest value to that value,
        highest_month to current_month.
```

# **Step 6** Trace the loop with typical examples.

Hand-trace your loop code, as described in Section 4.2. Choose example values that are not too complex—executing the loop 3–5 times is enough to check for the most common errors. Pay special attention when entering the loop for the first and last time.

Sometimes, you want to make a slight modification to make tracing feasible. For example, when hand-tracing the investment doubling problem, use an interest rate of 20 percent rather than 5 percent. When hand-tracing the temperature loop, use 4 data values, not 12.

Let's say the data are 22.6 36.6 44.5 24.2. Here is the walkthrough:

| current month | current value | highest month | highest value |
|---|---|---|---|
| 2 | 36.6 | 2 | 22.6 |
| 3 | 44.5 | 3 | 36.6 |
| 4 | 24.2 | | 44.5 |

The trace demonstrates that **highest month** and **highest value** are properly set.

# **Step 7** Implement the loop in C++.

Here's the loop for our example. Exercise P4.4 asks you to complete the program.

```
double highest_value;
cin >> highest_value;
int highest_month = 1;
for (int current_month = 2; current_month <= 12; current_month++)
{
    double next_value;
    cin >> next_value;
    if (next_value > highest_value)
    {
        highest_value = next_value;
        highest_month = current_month;
    }
}
cout << highest_month << endl;
```

# WORKED EXAMPLE 4.1 Credit Card Processing

This Worked Example uses a loop to remove spaces from a credit card number.

![](bbox=[0.08, 0.8, 0.22, 0.87])

![](bbox=[0.69, 0.78, 0.89, 0.87])