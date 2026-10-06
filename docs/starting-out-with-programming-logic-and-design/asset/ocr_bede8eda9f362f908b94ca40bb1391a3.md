# 2.3 Variable Assignment and Calculations

# In the Spotlight:
Calculating Cell Phone Overage Fees

Suppose your cell calling plan allows you to use 700 minutes per month. If you use more than this in a month, and you are charged an excess fee of 35 cents for each excess minute. Your phone shows the number of excess minutes that you have used in the current month, but it does not show how much your overage is. Until, you've been doing the math old-fashioned way (with pencil and paper, or with a calculator), but you would like to be able to enter the number of excess minutes, and have the program perform the calculation for you.

First, you want to make sure that you understand the steps that the program must perform. It will be helpful if you look closely at the way you are solving this problem, using only paper and pencil, or calculator:

# Manual Algorithm (Using pencil and paper, or calculator)

+   1. Get the number of excess minutes that you have used.
2. Multiply the number of excess minutes by 0.35.
3. The result of the calculation is your current overage fee.

Ask yourself the following questions about this algorithm:

> Question:
What do I need to perform this algorithm?
Answer:
I need the number of excess minutes.

> Question:
What must I do with the input?
Answer:
I multiply the input (the number of excess minutes) by 0.35. The result of that calculation is the overage fee.

> Question:
What output must I produce?
Answer:
The overage fee.

Now that you have identified the input, the process that must be performed, and the output, you can write the general steps of the program's algorithm:

# Computer Algorithm

+   1. Get the number of excess minutes as input.
2. Calculate the overage fee by multiplying the number of excess minutes by 0.35.
3. Display the overage fee.

In Step 1 of the computer algorithm, the program gets the number of excess minutes from the user. Any program needs the user to enter a piece of data, and it does two things: (1) it displays a message prompting the user for the piece of data, and (2) reads the data that the user enters on the keyboard, and stores that data in a variable. In pseudocode, Step 1 of the algorithm will look like this:

```
Display "Enter the number of excess minutes.
Input excessMinutes
```

Notice that the Input statement stores the value entered by the user in a variable named excessMinutes.