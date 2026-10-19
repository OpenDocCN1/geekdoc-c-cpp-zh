# Decrementing the Counter Variable

Step 3-6: Change the header of the loop as follows to decrement the counter variable:
for (int year = 5; year >= 1; year = year - 1)
Run the form. The value of year changes from 5 to 1, as follows:

| years | Investment Value |
| --- | --- |
| 5 | $10,700.00 |
| 4 | $22,149.00 |
| 3 | $34,399.43 |
| 2 | $47,507.39 |
| 1 | $61,532.91 |

# Review Questions

4.6 What would be the output of the following program?

```
int population = 65000;
for (int year = 2016; year <= 2018; year = year + 1)
{
    population = population + 1000;
    lstOutput.Items.Add(year + " " + population.ToString());
}
```

4.7 What would be the output of the following program?

```
int population = 65000;
for (int yr = 2018; yr > 2016; yr = yr - 1)
{
    population = population - 1000;
    lstDisplay.Items.Add(yr + " " + population.ToString());
}
```

# 4.6 The break and continue Statements

The break and continue statements let you deviate from the normal processing of a loop.

# The break Statement

You may jump out of a loop using the break statement.

Step 3-7: Modify the code by adding an if statement and a break statement, as shown in Figure 4-16, to break out of the loop, if investmentValue exceeds 100,000. Copy the display statement from line 42 to line 47 as shown, and make sure year is declared outside the loop.