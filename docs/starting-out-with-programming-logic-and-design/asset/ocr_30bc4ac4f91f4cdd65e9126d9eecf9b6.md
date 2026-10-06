# 5.4 Calculating a Running Total 209

5.15 Look at the following pseudocode. If it were a real program, what would it display?

```
Declare Integer counter
For counter = 0 To 500 Step 100
  Display counter
End For
```

5.16 Look at the following pseudocode. If it were a real program, what would it display?

```
Declare Integer counter = 1
Constant Integer MAX = 8
While counter <= MAX
  Display counter
  Set counter = counter + 1
End While
```

5.17 Look at the following pseudocode. If it were a real program, what would it display?

```
Declare Integer counter = 1
Constant Integer MAX = 7
While counter <= MAX
  Display counter
  Set counter = counter + 2
End While
```

5.18 Look at the following pseudocode. If it were a real program, what would it display?

```
Declare Integer counter
Constant Integer MIN = 1
For counter = 5 To Min Step -1
  Display counter
End For
```

# Calculating a Running Total

> CONCEPT: A running total is a sum of numbers that accumulates with each iteration of a loop. The variable used to keep the running total is called an accumulator.

Many programming tasks require you to calculate the total of a series of numbers. For example, suppose you are writing a program that calculates a business's total sales for a week. The program would read the sales for each day as input and calculate the total of numbers.

Programs that calculate the total of a series of numbers typically use two elements:

+   - A loop that reads each number in the series.
- A variable that accumulates the total of the numbers as they are read.