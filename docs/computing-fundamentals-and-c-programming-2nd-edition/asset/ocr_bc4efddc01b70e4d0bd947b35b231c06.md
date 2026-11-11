# ### 6.4.1 Inputting Integer Numbers

The field specification for reading an integer number is:

```
```
% w d
```
```

The percentage sign (%) indicates that a conversion specification follows. **w** is an integer number that specifies the *field width* of the number to be read and **d**, known as data type character, indicates that the number to be read is in integer mode. Consider the following example:

```
```c
scanf("%2d %5d", &num1, &num2);
```
```

Data line:

```
```
50 31426
```
```

The value 50 is assigned to **num1** and 31426 to **num2**. Suppose the input data is as follows:

```
```
31426 50
```
```

The variable **num1** will be assigned 31 (because of %2d) and **num2** will be assigned 426 (unread part of 31426). The value 50 that is unread will be assigned to the first variable in the next **scanf** call. This kind of errors may be eliminated if we use the field specifications without the field width specifications. That is, the statement

```
```c
scanf("%d %d", &num1, &num2);
```
```

will read the data

```
```
31426 50
```
```

correctly and assign 31426 to **num1** and 50 to **num2**.

Input data items must be separated by spaces, tabs or newlines. Punctuation marks do not count as separators. When the **scanf** function searches the input data line for a value to be read, it will always bypass any white space characters.

What happens if we enter a floating point number instead of an integer? The fractional part may be stripped away! Also, **scanf** may skip reading further input.

When the **scanf** reads a particular value, reading of the value will be terminated as soon as the number of characters specified by the field width is reached (if specified) or until a character that is not valid for the value being read is encountered. In the case of integers, valid characters are an optionally signed sequence of digits.

An input field may be skipped by specifying `*` in the place of field width. For example, the statement

```
```c
scanf("%*d %*d %d", &a, &b)
```
```

will assign the data

```
```
123 456 789
```
```

as follows:

```
```
123 to a
456 skipped (because of *)
789 to b
```
```

The data type character **d** may be preceded by ‘**l**’ (letter ell) to read long integers and **h** to read short integers.

> > **Note** *We have provided white space between the field specifications. These spaces are not necessary with the numeric input, but it is a good practice to include them.*