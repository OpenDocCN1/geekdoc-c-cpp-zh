# 5.3 Count-Controlled Loops and the For Statement

In this loop, the starting value of the counter variable is 0, and its ending value is 100. The Step clause specifies a step value of 10, which means that 10 is added to the counter at the end of each iteration. During the first iteration, counter is 0, during the second iteration, counter is 10, during the third iteration, counter is 20, and so forth.

The pseudocode in Program 5-10 gives another demonstration. The program displays all of the numbers from 1 through 11.

![](bbox=[0.315, 0.233, 0.355, 0.273])

```
// Declare a counter variable
Declare Integer counter

// Constant for the maximum value
Constant Integer MAX_VALUE = 11

// Display the odd numbers from 1 through 11
For counter = 1 To MAX_VALUE Step 2
    Display counter
End For
```

# Program Output

+   1
3
5
7
9
11

# In the Spotlight:
Designing a Count-Controlled Loop with the For Statement

Your friend Amanda just inherited a European sports car from her uncle, Amanda lives in the United States and she is afraid she will get a speeding ticket because the car's speedometer works in kilometers per hour. She asked you to write a program that displays a table of speeds in kilometers per hour with their values in miles per hour. The formula for converting kilometers per hour to miles per hour is:

> MPH = KPH × 0.6214

In the formula, MPH is the speed in miles per hour and KPH is the speed in kilometers per hour.