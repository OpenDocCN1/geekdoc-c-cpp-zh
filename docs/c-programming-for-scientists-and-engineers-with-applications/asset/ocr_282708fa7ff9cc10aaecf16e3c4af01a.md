# Input and Output

"enter key" is pushed the characters contained in the buffer are displayed as shown. The enter key carriage return indicates an end-of-file.

GetChar( ) and putchar( ) are the basic character input/output functions in the C language. Since everything typed on a keyboard or displayed on a monitor or printed on is in the form of characters that are readable by people, the computer does all input and output character-by-character. However if these were the only input and output functions available to the programmer, every programmer would have to develop numeric input/output routines in order to be able to process numbers.

If the stream contained the characters -234 preceded by a blank, the programmer would have to determine that the number is negative and then accumulate its value by using the iterative formula as follows:

```
-1(10 * ( 10 * (0 + 2) + 3) + 4)
```

The algorithm for this is as follows:

```
For each leading blank
Ignore it
End for
```

```
value = 0
if next character is a minus sign
sign = -1
else
sign = 1
```

```
For each digit
value = 10 * value + digit
End for
```

```
value = value * sign
```

For every programmer to develop a private library of input/output functions, or to rewrite them every time a program is written, is an unnecessary duplication of of