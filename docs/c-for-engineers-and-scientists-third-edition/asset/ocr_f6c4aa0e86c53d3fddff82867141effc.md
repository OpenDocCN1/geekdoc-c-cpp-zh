4. (Electrical Eng.) Write a program that stores the following resistance values in an array named resistance: 16, 27, 39, 56, and 81. Your program should also create two arrays named current and power, each capable of storing five double-precision numbers. Using a for loop and a cin statement, have your program accept five user-inputs in the current array when the program is run. Your program should store the product of the squares of the current array and the resistance array for. For example, use power[1] = resistance[1] * pow(current[1],2). Your program should display the following output (fill in the chart):

| Resistance | Current | Power |
|---|---|---|
| 16 | | |
| 27 | | |
| 39 | | |
| 56 | | |
| 81 | | |
| Total: | | |

5. (Practice) Write a declaration to store the string "This is a test" in an array named strtest. Include the declaration in a program to display the message, using the following loop:

```
for (i = 0; i < NUMDISPLAY; i++)
    cout << strtest[i];
```

NUMDISPLAY is a named constant for the number 14.

+   b. Modify the for statement in Exercise 5a to display only the array characters t, e, s, and t.

+   c. Include the array declaration written in Exercise 5a in a program that uses a cout statement to display the characters in the array. For example, the cout << strtest causes the string stored in the strtest array to be displayed. Using this statement requires the end-of-string marker, \0, as the last character in the array.

+   d. Repeat Exercise 5a, using a while loop. (Hint: Stop the loop when the \0 escape sequence is detected. The expression while (strtest[i] != '\0') can be used.)