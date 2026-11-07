
The preceding program works as follows. The statements in Lines 8 to 13 declare the variables used in the program. The statement in Line 14 prompts the user to enter the radius of the sphere, and the statement in Line 15 stores the radius in the variable sphereRadius. The statement in Line 17 uses the function pow to compute and store the volume of the sphere in the variable sphereVolume. The statement in Line 18 outputs the volume. The statement in Line 19 prompts the user to enter the coordinates of two points in the X-Y plane, and the statement in Line 20 stores the coordinates in the variables point1x, point1y, point2x, and point2y, respectively. The statement in Line 22 uses the functions sqrt and pow to determine the distance between the points. The statement in Line 23 outputs the distance between the points. The statement in Line 24 stores the string "Programming with C++" in str. The statement in Line 25 uses the string function length to determine and output the length of str. Note how the function length is used. Later in this chapter we will explain the meaning of expressions such as str.length().

Because I/O is fundamental to any programming language and because writing instructions to perform a specific I/O operation is not a job for everyone, every programming language provides a set of useful functions to perform specific I/O operations. In the remainder of this chapter, you will learn how to use some of these functions in a program. As a programmer, you must pay close attention to how these functions are used so that you can get the most out of them. The first function you will learn about here is the function get.

## cin and the get Function

As you have seen, the extraction operator skips all leading whitespace characters when scanning for the next input value. Consider the variable declarations:

```
char ch1, ch2;
int num;
```

and the input:

```
A 25
```

Now consider the following statement:

```
cin >> ch1 >> ch2 >> num;
```

When the computer executes this statement, 'A' is stored in ch1, the blank is skipped by the extraction operator >>, the character '2' is stored in ch2, and 5 is stored in num. However, what if you intended to store 'A' in ch1, the blank in ch2, and 25 in num? It is clear that you cannot use the extraction operator >> to input this data.

As stated earlier, sometimes you need to process the entire input, including whitespace characters, such as blanks and the newline character. For example, suppose you want to process the entered data on a line-by-line basis. Because the extraction operator >> skips the newline character and unless the program captures the newline character, the computer does not know where one line ends and the next begins.

The variable `cin` can access the stream function `get`, which is used to read character data. The `get` function inputs the very next character, including whitespace characters, from the input stream and stores it in the memory location indicated by its argument. The function `get` comes in many forms. Next, we discuss the one that is used to read a character.

The syntax of `cin`, together with the `get` function to read a character, follows:

```
cin.get(varChar);
```

In the `cin.get` statement, `varChar` is a `char` variable. `varChar`, which appears in parentheses following the function name, is called the **argument** or **parameter** of the function. The effect of the preceding statement would be to store the next input character in the variable `varChar`.

Now consider the following input again:

```
    A 25
```

To store 'A' in `ch1`, the blank in `ch2`, and `25` in `num`, you can effectively use the `get` function as follows:

```
cin.get(ch1);
cin.get(ch2);
cin >> num;
```

Because this form of the `get` function has only one argument and reads only one character and you need to read two characters from the input stream, you need to call this function twice. Notice that you cannot use the `get` function to read data into the variable `num` because `num` is an `int` variable. The preceding form of the `get` function reads values of only the `char` data type.

The preceding set of `cin.get` statements is equivalent to the following statements:

```
cin >> ch1;
cin.get(ch2);
cin >> num;
```

> **NOTE**
>
> The function `get` has other forms, one of which you will study in Chapter 8.
> For the next few chapters, you need only the form of the function `get` introduced here.

## `cin` and the `ignore` Function

When you want to process only partial data (say, within a line), you can use the stream function `ignore` to discard a portion of the input. The syntax to use the function `ignore` is:

```
cin.ignore(intExp, chExp);
```

Here, **intExp** is an integer expression yielding an integer value, and **chExp** is a char expression yielding a char value. In fact, the value of the expression **intExp** specifies the maximum number of characters to be ignored in a line.

Suppose **intExp** yields a value of, say 100. This statement says to ignore the next 100 characters or ignore the input until it encounters the character specified by **chExp**, whichever comes first. To be specific, consider the following statement:

```
cin.ignore(100, '\n');
```

When this statement executes, it ignores either the next 100 characters or all characters until the newline character is found, whichever comes first. For example, if the next 120 characters do not contain the newline character, then only the first 100 characters are discarded and the next input data is the character 101. However, if the 75th character is the newline character, then the first 75 characters are discarded and the next input data is the 76th character. Similarly, the execution of the statement:

```
cin.ignore(100, 'A');
```

results in ignoring the first 100 characters or all characters until the character 'A' is found, whichever comes first.

### EXAMPLE 3-5

Consider the declaration:

```
int a, b;
```

and the input:

```
25 67 89 43 72
12 78 34
```

Now consider the following statements:

```
cin >> a;
cin.ignore(100, '\n');
cin >> b;
```

The first statement, `cin >> a;`, stores 25 in a. The second statement, `cin.ignore(100, '\n');`, discards all the remaining numbers in the first line. The third statement, `cin >> b;`, stores 12 (from the next line) in b.

### EXAMPLE 3-6

Consider the declaration:

```
char ch1, ch2;
```

and the input:

```
Hello there. My name is Mickey.
```

- a. Consider the following statements:

    ```
    cin >> ch1;
    cin.ignore(100, '.');
    cin >> ch2;
    ```

    The first statement, `cin >> ch1;`, stores 'H' in ch1. The second statement, `cin.ignore(100, '.');`, results in discarding all characters until . (period). The third statement, `cin >> ch2;`, stores the character 'M' (from the same line) in ch2. (Remember that the extraction operator >> skips all leading whitespace characters. Thus, the extraction operator skips the space after . (period) and stores 'M' in ch2.)

- b. Suppose that we have the following statements:

    ```
    cin >> ch1;
    cin.ignore(5, '.');
    cin >> ch2;
    ```

    The first statement, `cin >> ch1;`, stores 'H' in ch1. The second statement, `cin.ignore(5, '.');`, results in discarding the next five characters, that is, until t. The third statement, `cin >> ch2;`, stores the character 't' (from the same line) in ch2.

When the function ignore is used without any arguments, then it only skips the very next character. For example, the following statement will skip the very next character:

```
cin.ignore();
```

This statement is typically used to skip the newline character.

## The putback and peek Functions

Suppose you are processing data that is a mixture of numbers and characters. Moreover, the numbers must be read and processed as numbers. You have also looked at many sets of sample data and cannot determine whether the next input is a character or a number. You could read the entire data set character by character and check whether a certain character is a digit. If a digit is found, you could then read the remaining digits of the number and somehow convert these characters into numbers. This programming code would be somewhat complex. Fortunately, C++ provides two very useful stream functions that can be used effectively in these types of situations.

The stream function putback lets you put the last character extracted from the input stream by the get function back into the input stream. The stream function peek looks into the input stream and tells you what the next character is without removing it from the input stream. By using these functions, after determining that the next input is a number, you can read it as a number. You do not have to read the digits of the number as characters and then convert these characters to that number.
