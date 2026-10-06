```
100.25 S Set Accumulator to 100.25
= 100.250000 Multiply by 4
4 * = 401.000000 End of program
0 E = 401.000000
End of Calculations.
```

Make sure that the program detects division by 0 and also checks for unknown operators. Use the Calculator class developed in Program 6.8 for performing your calculations.
Note: Remember to use a space character in your scanf format string (e.g., "%f %c") to skip whitespace characters in the input.

+   5. We developed Program 5.9 to reverse the digits of an integer typed in from the terminal. However, this program does not function well if you type in a negative number. Find out what happens in such a case, and then modify the program so that negative numbers are correctly handled. By this, we mean if the number -8645 were typed in, for example, the output of the program should be 5468-.

+   6. Write a program that takes an integer keyed in from the terminal and extracts and displays each digit of the integer in English. So if the user types in 932, the program should display the following:

nine
tthree
two

(Remember to display zero if the user types in just 0.) Note: This exercise is a hard one!

+   7. Program 6.10 has several inefficiencies. One inefficiency results from checking even numbers. Because any even