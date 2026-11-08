| Statement | Input | Value Stored in Memory |
|---|---|---|
| 8. `cin >> a >> b;` | `4 60` | `a = 4, b = 60` |
| 9. `cin >> a >> z;` | `46 32.4 68` | `a = 46, z = 32.4, 68 is held for later input` |

# EXAMPLE 3-2

Suppose you have the following variable declarations:

```
int a;
double z;
char ch;
```

The following statements show how the extraction operator `>>` works.

| Statement | Input | Value Stored in Memory |
|---|---|---|
| 1. `cin >> a >> ch >> z;` | `57 A 26.9` | `a = 57, ch = 'A', z = 26.9` |
| 2. `cin >> a >> ch >> z;` | `57 A`<br>`26.9` | `a = 57, ch = 'A', z = 26.9` |
| 3. `cin >> a >> ch >> z;` | `57`<br>`A`<br>`26.9` | `a = 57, ch = 'A', z = 26.9` |
| 4. `cin >> a >> ch >> z;` | `57A26.9` | `a = 57, ch = 'A', z = 26.9` |

Note that for statements 1 through 4, the input statement is the same; however, the data is entered differently. For statement 1, data is entered on the same line separated by blanks. For statement 2, data is entered on two lines: the first two input values are separated by two blank spaces, and the third input is on the next line. For statement 3, all three input values are separated by lines, and for statement 4, all three input values are on the same line, but there is no space between them. Note that the second input is a non-numeric character. These statements work as follows.

Statements 1, 2, and 3 are easy to follow. Let us look at statement 4.

In statement 4, first the extraction operator `>>` extracts 57 from the input stream and stores it in a. Then, the extraction operator `>>` extracts the character 'A' from the input stream and stores it in ch. Next, 26.9 is extracted and stored in z.

Note that statements 1, 2, and 3 illustrate that regardless of whether the input is separated by blanks or by lines, the extraction operator `>>` always finds the next input.