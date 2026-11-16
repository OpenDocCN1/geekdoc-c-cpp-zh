
Character constants have the type `int` whose values are the integer encodings of the characters in the target character set (ASCII – Unicode). For example:

```
'A' = 65
'a' = 97
'$' = 36
'5' = 53
'\n' = 10
'\t' = 9
'\0' = 0
```

## String Constants

String constants are a (possibly empty) sequence of characters enclosed in double quotes:

```
"Haley"
"Samantha"
"Yellow"
""
```

Note that string constants, unlike other constants, actually have a location in memory. For each string constant of N characters, there will be at run-time a statically allocated block of N+1 characters whose first N characters are initialized with the characters from the string and whose last character is the null character, '\0'. The null character is used so programs can conveniently find the end of a string.

We can now see why the character 'a' is not the same as the string "a". The character 'a' represents a single ASCII character, while the string "a" contains an array of two characters that contains the ASCII character 'a' along with the null character '\0'.

The shortest string is the null string and is represented as "". It is stored in memory as the single null character '\0'.

## Mixing Data Types

Numerical data types can be converted from one type to another. For example:

- int can be converted to double or float
- int can be converted to char (may cause some loss of information)
- char can be converted to int
- float can be converted to double
- double can be converted to float (may cause some loss of accuracy)
- double or float can be converted to int (but fractional values will be truncated)

## Implicit (automatic) Conversions

Whenever different data types are used in an assignment expression, the data type on the right side of the expression is converted to the data type on the left side. For example:

```
int num;
char c;
:
num = c;
```

Here, c is converted to an int and then assigned to num. Because a char data type needs fewer bits than an int, c is normally zero-filled on the left during conversion.

However, when you make the assignment:

```
c = num;
```

the integer num is assigned to a char and any excess bits in num are discarded before assignment to c. In fact, the most significant bits are discarded so information will be lost!

## Performing Binary Operations on Mixed Data Types

If you perform binary operation on two different data types, the compiler will convert the data type that requires the fewer number of bits to the data type that requires the greatest number of bits for internal storage.

For example, if an int and a double are multiplied, the int is converted to a double before the multiplication because the double requires a larger number of bits for its internal representation than does an int. The result returned from the operation is converted to the data type that requires the largest number of bits for its representation, in this case a double.

See if you can figure out the output produced from the following program:

```
// mixed.c

#include <stdio.h>

int main(void) {
    float f1 = 123.125, f2;
    int i1, i2 = 150;
    char c = 'a';
    // float to int conversion
    i1 = f1;
    printf("%d\n", i1);
    // int to float conversion
    f1 = i2;
    printf("%f\n", f1);
    // int divided by int
    f1 = i2 / 100;
    printf("%f\n", f1);
    // int divided by float
    f2 = i2 / 100.0;
    printf("%f\n", f2);
    return 0;
}
```

Here's the output:

```
123
150.000000
1.000000
1.500000
```

## Can you see why?

Note that integer division truncates towards zero:

```
int a, b;
:
a = 1/3;   // produces 0
b = 6/7;   // produces 0
```

However, if either operand of the division is a float, both operands are converted to float:

```
float w, x, y, z;
:
w = 1.0 / 3.0;   // 0.333333
x = 1.0 / 3;     // 0.333333
y = 6.0 / 7.0;   // 0.857143
z = 6 / 7.0;     // 0.857143
```

## Explicit (automatic) Conversions

The cast operator converts (casts) the value of a variable into a type that is different from the original type of the variable. The cast is specified by giving the cast type in parentheses followed by the expression to be cast:

```
(cast-type) expression
```

For example:

```
int x;
float y;
:
y = (float) x;
```

This converts the integer value of `x` to its corresponding `float` value and assigns that value to `y`. Note that the conversion does not change the value or the type of `x`. The conversion is held in temporary storage.

We normally cast a variable to ensure that the arithmetic is carried out with the type of the left-hand side:

```
a = (int) 17.7 * 2;
```

The result is:

```
a = 34;
```

We can round a variable to an integer by first adding 0.5 and then casting to an `int`:

```
a = (int) (val + 0.5);
```

A typical use of cast is in forcing division to return a real number when both operands are integers:

```
average = (float) sum / num;
```

Without the cast, truncated integer division is performed, since both `sum` and `num` are integers.

## scanf() Function

scanf() is a function in the standard library which allows you to input values into a program from standard input (keyboard). It's usually used to input numerical data using formats similar to the printf() statement.

Like printf(), scanf() has a control string, followed by the list of items to be read. However scanf() wants to know the addresses of the items to be read, since it is a function which will change those values. Therefore the names of variables are preceded by the & sign. Note that character strings are an exception to this. Since a string is already a character pointer, we give the names of string variables unmodified by a leading & (more on strings later).

In the expression:

```
scanf("%d %d", &x, &y);
```

the arguments &x and &y tell scanf() where to store the data that it reads. & is an operator in C which gives the address of its operand, i.e., &x gives the address of x. Note that the arguments to the scanf() function MUST be pointers to the locations in memory where the input is to be stored.

Here are scanf() format codes:

| Code | Meaning |
|---|---|
| %c | read a character |
| %d | read a decimal integer |
| %ld | reads a long decimal integer |
| %f | read a floating point number |
| %lf | reads a double |
| %h | read a short integer |
| %x | read a hexadecimal number |
| %s | read a string |

Here's an example of the use of `scanf():`

```
// scanf.c

#include <stdio.h>

int main(void) {
    int i;
    float f;
    char buf[32];

    printf("Enter an integer, float, and string: ");
    scanf("%d %f %s", &i, &f, buf);
    return 0;
}
```

Input line:

```
25   3.14159   Samantha
```

The three input fields may be separated by as many blanks, tabs, and newlines (whitespace characters) as desired.

Note that the argument `buf` did not need an `&` before it. Why?

When arrays are passed as arguments in functions, they are always passed by reference and therefore a pointer to the array (or the first address within the array) is actually being passed.

Also note that `scanf()` skips any leading whitespace characters in the input (except when using the `%c` format specifier).

When the `%s` specifier is used, the value to be read is a sequence of characters that begins with the first non-whitespace character and is terminated by the first whitespace character. The corresponding argument is a pointer to a character array, which must contain enough locations to contain all the characters that are read plus the null character that is added to the end of the string automatically by the function.

The `scanf()` function can also take an optional modifier between the `%` and the format character that determines the field-width number used to indicate the maximum number of positions or digits to expect in an argument (or that a field occupies).

## For example:

```
scanf("%d %10s", &num, buf);

1234string        1234        string
123456string      1234        56string
9999string        9999        string
```

If a field-width modifier is supplied, the specified number of characters is read, unless a whitespace character is encountered first.

Note that when scanf() reads in a particular value, reading of the value will terminate as soon as a character that is not valid for the value being read is encountered (or as soon as the number of characters specified by the field width is reached, if specified).

Any non-format characters specified in the format string of scanf() is to be expected on the input. For example, to enter the current time from terminal we can use:

```
scanf("%d:%d:%d", &hour, &min, &sec);
```

The : specify that colons are expected as separators between the three integer values.

White space characters inside a format string match an arbitrary number of whitespace characters on the input:

```
scanf("%d%c", &i, &c);

input:
29 w

assign:
29 to i
space to c
```
