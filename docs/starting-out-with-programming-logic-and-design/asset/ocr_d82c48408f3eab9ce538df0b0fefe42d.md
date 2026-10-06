# Program 5-9

```
// Variables
Declare Integer counter, square
// Constant for the maximum value
Constant Integer MAX_VALUE = 10

// Display table headings.
Display "Number", Tab, "Square"
----------------------

// Display the numbers 1 through 10
// their squares.
For counter = 1 To MAX_VALUE
  // Calculate number squared.
  Set square = counter2
  // Display number and number squared.
  Display counter, Tab, square
End For
```

# Program Output

| Number | Square |
| --- | --- |
| 1 | 1 |
| 2 | 4 |
| 3 | 9 |
| 4 | 16 |
| 5 | 25 |
| 6 | 36 |
| 7 | 49 |
| 8 | 64 |
| 9 | 81 |
| 10 | 100 |

# Incrementing by Values Other Than 1

The amount by which the counter variable is incremented in a For loop is known as the step amount. By default, the step amount is 1. Most languages provide a way to change the step amount. This gives you the ability to increment the counter variable by any value you wish.

In pseudocode, we use the optional Step clause to specify a step value in a For loop. For example, look at the following pseudocode:

```
For counter = 0 To 100 Step 10
  Display counter
End For
```