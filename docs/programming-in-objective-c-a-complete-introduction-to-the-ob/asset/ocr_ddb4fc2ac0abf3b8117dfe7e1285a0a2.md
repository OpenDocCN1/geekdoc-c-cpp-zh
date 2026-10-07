# Chapter 5 Program Looping

Features,” the pre- or post- nature of the operator comes into play when used in more complex expressions.

You might have noticed that the line of output from Program 5.3 does not line up. You can correct this minor annoyance by substituting the NSLog statement in place of the corresponding statement from Program 5.3:

```
NSLog("%2i i, n, triangularNumber);
```

To verify that this change solves the problem, here’s the output from the modified program (called Program 5.3A).

# Program 5.3A Output

TABLE OF TRIANGULAR NUMBERS
| n | Sum from 1 to n |
|---|---|
| 1 | 1 |
| 2 | 3 |
| 3 | 6 |
| 4 | 10 |
| 5 | 15 |
| 6 | 21 |
| 7 | 28 |
| 8 | 36 |
| 9 | 45 |
| 10 | 55 |

The change made to the NSLog statement is is the inclusion of a field width specification. The characters %2i tell the NSLog routine not only that you want to display the value of an integer at that particular point, but also the size of the integer to be displayed at least two columns in the display. Any integer that would normally take up less than two columns (that is, the integers 0–9) will be displayed with a leading space. This is known as *right justification*.

Thus, by using a field width specification of %2i, you guarantee that at least two columns will be used for displaying the value of n; you also ensure that the values of triangularNumber will be aligned.

# Keyboard Input

Program 5.2 calculates the 200th triangular number, and nothing more. What if you wanted to calculate the 50th or the 100th triangular number instead? Well, if that were the case, you would have to change the program so that the for loop would be executed the correct number of times. You would also have to change the NSLog statement to display the correct message.

An easier solution might be to somehow ask the program which triangular number you want to calculate. Then, after you had given your answer, the program could calculate the desired triangular number. You can effect such a solution by using a routine-