
| 6. | Relational | < | Less than |
|---|---|---|---|
| | | <= | Less than or equal to |
| | | > | Greater than |
| | | >= | Greater than or equal to |
| 7. | Equality | == | Equal to |
| | | != | Not equal to |
| 8. | | & | Bitwise AND |
| 9. | | ^ | Bitwise XOR |
| 10. | | \| | Bitwise OR |
| 11. | | && | Logical AND |
| 12. | | \|\| | Logical OR |
| 13. | Conditional | ?: | |
| 14. | Assignment | = | Simple assignment |
| | | *= | Assign product |
| | | /= | Assign quotient |
| | | %= | Assign remainder (modulus) |
| | | += | Assign sum |
| | | -= | Assign difference |
| | | &= | Assign Bitwise AND |
| | | ^= | Assign Bitwise XOR |
| | | \|= | Assign Bitwise OR |
| | | <<= | Assign left shift |
| | | >>= | Assign right shift |
| 15. | Comma | , | Evaluate |

## Operators Homework

1. Write a single C statement to accomplish each of the following tasks:

- a) Assign the product of x and y to z and increment the value of y by 1 after the calculation.

  ```
  z = x * (y++);
  ```

- b) Multiply value by 5 using the += operator.

  ```
  Value += 5;
  ```

- c) Decrement variable x by 1, then subtract it from variable result.

  ```
  result -= --x;
  ```

- d) Add variable x to variable total, then increment x by 1.

  ```
  total += x++
  ```

2. Show the output produced by each of the following program fragments.
Assume that i, j, k are int variables.

- a)

  ```
  i = 5; j = 3;
  printf("%d %d", i / j, i % j);
  ```

  Output: 1 2

- b)

  ```
  i = 2; j = 3;
  printf("%d %d", (i + 10) % j);
  ```

  Output: 0

- c)

  ```
  i = 7; j = 8; k = 9;
  printf("%d %d", (i + 10) % k / j);
  ```

  Output: 1

3. Show the output produced by each of the following program fragments.
Assume that i, j, k are int variables.

- a)

  ```
  i = 7; j = 8;
  i *= j + 1;
  printf("%d %d", i, j);
  ```

  Output: 63 8

- b)

  ```
  i = j = k = 1;
  i += j += k;
  printf("%d %d %d", i, j, k);
  ```

  Output: 3 2 1

4. Show the output produced by each of the following program fragments. Assume that i, j, k are int variables.

```
i = 5;
j = (++i * 3) - 2;
printf("%d %d", i, j);
```

```
i = 5;
j = 3 - 2 * i++;
printf("%d %d", i, j);
```

```
i = 10; j = 5;
printf("%d ", i++ - ++j);
printf("%d %d", i, j);
```

5. Supply parentheses to show how a C compiler would interpret each of the following expressions.

```
((a * b) - (c * d) + e)
```

```
(((a / b) % c) / d)
```

6. Give the values of i and j after each of the following expression statements has been executed. Assume that i has the value 1 initially and j has the value 2.

```
i += j;
```

```
i--;
```

```
i * j / i;
```

```
i % ++j;
```

7. Use De Morgan's Laws to write equivalent expressions for each of the following:

```
!( x < 8 ) && !( y >= 3 )
```

```
!( x == y ) || !( z != 2 )
```

```
!( ( x <= 3 ) && ( y > 7 ) )
```

```
!( ( x > 2 ) || ( y <= 4 ) )
```

## Weight Lab

Our weight on different planets in the solar system will differ due to the varying size and mass of each of the planets. Write a C program, weight.c, to compute the weight of a 200 pound person on the following planets, based on the data below:

| Planet | Percent of Earth Weight |
| :--- | :--- |
| Mercury | 37.8% |
| Venus | 90.7% |
| Mars | 37.7% |
| Jupiter | 236.0% |
| Saturn | 91.6% |
| Uranus | 88.9% |
| Neptune | 112.0% |

The program should generate the following outputs:

```
Mercury: xxx.x
Venus: xxx.x
Mars: xxx.x
Jupiter: xxx.x
Saturn: xxx.x
Uranus: xxx.x
Neptune: xxx.x
```

Your program should right-justify the planet names as shown above and present the output to one decimal place. Be sure to line up the decimal points. Use the following guidelines to develop your program:

- Declare your variables with appropriate data types.
- Assign values to your variables.
- Perform your calculations.
- Generate appropriate output.

### Points to Remember:

Make sure you are creating a C program and not a C++ program. The .c suffix to your source code will invoke the C compiler while the .cpp suffix will invoke the C++ compiler. As this is a class in C and not C++, please make sure your source code uses the .c suffix.

You should not be using any global variables in your program. A global variable is a variable declared outside of main().

Output your calculations to one decimal place.

Output from your program should be sent to the terminal window (your screen) as well as the requested data.txt output file. Be sure to read the document on Capturing Program Output. Your full name and Palomar ID number must appear as a comment in the source file that contains main(). Be sure to include the cseis.txt output file in your zip archive.

![](img/7f36c52b5170b89b142dbb7b1ea4666b_106_0.png)

## Character Constant Lab

Write a C program, `char.c`, which prints the numerical value of the special character constants given below. Don't just look up the codes and print them directly from your program. You should have your program output the values of the character constants by using them as string literals within your `printf()` statements.

Your output should be presented in a neat, orderly, tabular format as shown below:

| Char Constant | Description | Value |
|---|---|---|
| `'\n'` | newline | 10 |
| `'\t'` | horizontal tab | 9 |
| `'\v'` | vertical tab | 11 |
| `'\b'` | backspace | 8 |
| `'\r'` | carriage return | 13 |
| `'\f'` | form feed | 12 |
| `` `\` `` | backslash | 92 |
| `'\''` | single quote (apostrophe) | 39 |
| `'"` | double quote | 34 |
| `'\0'` | null | 0 |

Use the following guidelines to develop your program:

- Declare your variables with appropriate data types.
- Assign values to your variables.
- Perform your calculations.
- Generate appropriate output.

### Points to Remember:

Make sure you are creating a C program and not a C++ program. The `.c` suffix to your source code will invoke the C compiler while the `.cpp` suffix will invoke the C++ compiler. As this is a class in C and not C++, please make sure your source code uses the `.c` suffix.

You should not be using any global variables in your program. A global variable is a variable declared outside of main().

Output from your program should be sent to the terminal window (your screen) as well as the requested csis.txt output file. Be sure to read the document on Capturing Program Output. Your full name and Palomar ID number must appear as a comment in the source file that contains main(). Be sure to include the csis.txt output file in your zip archive.

## Change Lab

Construct a C program, change.c, which computes the minimum number of bills and coins needed to make change for a particular purchase. The cost of the item is $21.17 and the amount tendered is $100.00. These values should be built into your program using assignment statements rather than input into the program during program runtime. Your program should indicate how many bills and coins of each denomination are needed for the change. You should make use of the following denominations:

- Bills: twenty, ten, five, one
- Coins: quarter, dime, nickel, penny

Your program should make use of integer division as well as the modulus operator (%). Do not use subtraction in place of the modulus operator! Note that it will be easier to convert the cost and amount tendered into pennies so you can work with integers rather than doubles.

Use the following guidelines to develop your program:

- Declare your variables with appropriate data types.
- Assign values to your variables.
- Perform your calculations.
- Generate appropriate output.

### Points to Remember:

Make sure you are creating a C program and not a C++ program. The .c suffix to your source code will invoke the C compiler while the .cpp suffix will invoke the C++ compiler. As this is a class in C and not C++, please make sure your source code uses the .c suffix.

You should not be using any global variables in your program. A global variable is a variable declared outside of main().
