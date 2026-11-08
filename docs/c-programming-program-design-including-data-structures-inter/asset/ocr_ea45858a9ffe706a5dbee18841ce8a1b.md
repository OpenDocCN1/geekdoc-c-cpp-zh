# EXAMPLE 3-3

Suppose you have the following variable declarations:

```
int a;
double z;
char ch, ch1, ch2;
```

The following statements show how the extraction operator >> works.

| Statement | Input | Value Stored in Memory |
|---|---|---|
| 1. `cin >> z >> ch >> a;` | `36.78B34` | `z = 36.78, ch = 'B', a = 34` |
| 2. `cin >> z >> ch >> a;` | `36.78 B34` | `z = 36.78, ch = 'B', a = 34` |
| 3. `cin >> a >> b >> z;` | `11 34` | `a = 11, b = 34, computer waits for the next number` |
| 4. `cin >> a >> z;` | `78.49` | `a = 78, z = 0.49` |
| 5. `cin >> ch >> a;` | `256` | `ch = '2', a = 56` |
| 6. `cin >> a >> ch;` | `256` | `a = 256, computer waits for the input value for ch` |
| 7. `cin >> ch1 >> ch2;` | `A B` | `ch1 = 'A', ch2 = 'B'` |

In statement 1, because the first right-side operand of >> is a double variable, 36.78 is extracted from the input stream, and the value 36.78 is stored in z. Next, 'B' is extracted and stored in ch. Finally, 34 is extracted and stored in a. Statement 2 works similarly.

In statement 3, 11 is stored in a, and 34 is stored in b, but the input stream does not have enough input data to fill each variable. In this case, the computer waits (and waits, and waits…) for the next input to be entered. The computer does not continue to execute until the next value is entered.

In statement 4, the first right-side operand of the extraction operator >> is a variable of the type int, and the input is 78.49. Now for int variables, after inputting the digits of the number, the reading stops at the first whitespace character or a character other than a digit. Therefore, the operator >> stores 78 into a. The next right-side operand of >> is the variable z, which is of the type double. Therefore, the next operator >> stores the value .49 as 0.49 into z.

In statement 5, the first right-side operand of the extraction operator >> is a char variable, so the first nonwhitespace character, '2', is extracted from the input stream. The character '2' is stored in the variable ch. The next right-side operand of the extraction operator >> is an int variable, so the next input value, 56, is extracted and stored in a.