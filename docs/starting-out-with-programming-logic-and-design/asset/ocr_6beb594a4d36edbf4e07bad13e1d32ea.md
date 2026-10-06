# 5.4 Calculating a Running Total 211

```
// Explain what we are doing.
// Display "This program calculates the"
// Display "total of five numbers."

// Get five numbers and accumulate them.
For counter = 1 To 5
    Display "Enter a number."
    Input number
    Set total = total + number
End For

// Display the total of the numbers.
Display "The total is ", total
```

Program Output (with Input Shown in Bold)

This program calculates the
total of five numbers.
Enter a number.
2 [Enter]
Enter a number.
4 [Enter]
Enter a number.
6 [Enter]
Enter a number.
8 [Enter]
Enter a number.
10 [Enter]
The total is 30

First, let's look at the variable declarations. The number variable, declared in line 3, will be used to hold a number entered by the user. The total variable, declared in line 7, is the accumulator. Notice that it is initialized with the value 0. The counter variable, declared in line 10, will be used as a counter for the loop.

The For loop, in lines 17 through 21, does the work of gathering the numbers from the user and calculating their total. Line 18 prompts the user to enter a number, and line 19 updates it and stores it in the number variable. Then, the following statement in line 20 adds number to total:

```
Set total = total + number
```

After this statement executes, the value in the number variable will be added to the value in the total variable. When the loop finishes, the total variable will hold the sum of all the numbers that were added to it. This value is displayed in line 24. Figure 5-18.