# 6.1 Introduction to Functions: Generating Random Numbers

When this statement executes, the random function is called. The function generates a random number in the range of 1 through 10. That value is returned and then sent to the Display statement. As a result, a random number in the range of 1 through 10 will be displayed. Figure 6-4 illustrates this.

The pseudocode in Program 6-3 shows how you could simplify Program 6-2. This program displays five random numbers, but this program does not use a variable to hold those numbers. The random function's return value is sent directly to the Display statement in line 4.

# Figure 6-4 Displaying a random number

![](bbox=[0.395, 0.273, 0.605, 0.335])

A random number in the range of 1 through 10 will be displayed.

# Program 6-3

```
// Counter variable
// Declare Integer counter
// This loop displays five random numbers.
// For counter = 1 To 5
  Display random(1, 100)
End For
```

# Program Output

```
32
79
6
12
98
```

# In the Spotlight:

# Using Random Numbers

Dr. Kimura teaches an introductory statistics class, and has asked you to write a program that he can use to simulate the rolling of dice. The program should randomly generate two numbers in the range of 1 through 6 and display them. In your interview with Dr. Kimura, you learn that he would like to simulate several rolls of the dice, one after the other. You decide to write a loop that simulates one roll of the dice, and then asks the user whether another roll should be performed. As long as the user answers “y” for yes, the loop will repeat. Program 6-4 shows the pseud, and Figure 6-5 shows the flowchart.