
## Syntax

## The printf() Function

```c
#include <stdio.h>
printf(format-string,arguments,...);
```

printf() is a function that accepts a series of arguments, each applying to a conversion specifier in the given format string. printf() prints the formatted information to the standard output device, usually the display screen. When using printf(), you need to include the standard input/output header file, stdio.h. The format-string is required; however, arguments are optional. For each argument, there must be a conversion specifier. Table 7.2 lists the most commonly used conversion specifiers.

The format-string can also contain escape sequences. Table 7.1 lists the most frequently used escape sequences.

The following are examples of calls to printf() and their output:

### Example 1 Input

```c
#include <stdio.h>
int main( void )
{
printf("This is an example of something printed!");
    return 0;
}
```

### Example 1 Output

This is an example of something printed!

### Example 2 Input

```c
printf("this prints a character, %c\n number, %d\n floating \npoint, %%f", 'z', 123, 456.789);
```

### Example 2 Output

This prints a character, z
a number, 123
a floating point, 456.789

> You may notice in the second example, the printf() function uses a string that wraps to a second line. At the end of the first line, a forward slash (\) indicates the string continues to the next line. The compiler treats the two lines as one.

## Display Messages with puts()

The puts() function can also be used to display text messages on the screen, but it can't display numeric variables. The puts() function takes a single string as its argument and displays it, automatically adding a newline at the end. For example, the statement

```c
puts("Hello, world.");
```

performs the same action as

```c
printf("Hello, world.\n");
```

You can include escape sequences (including \n) in a string passed to puts(). They have the same effect as when they are used with puts(). (See Table 7.1 for the most common escape sequences.)

Just like printf(), any program that uses puts() should include the header file stdio.h. Note that stdio.h should be included only once in a program.

| DO | DON'T |
| --- | --- |
| use the puts() function instead of the printf() function whenever you want to print text but don't need to print any variables. | try to use conversion specifiers with the puts() statement. |

## Syntax

## The puts() Function

```c
#include <stdio.h>
puts(string);
```

puts() is a function that copies a string to the standard output device, usually the display screen. When you use puts(), include the standard input/output header file (stdio.h). puts() also appends a newline character to the end of the string that is printed. The format string can contain escape sequences. Table 7.1 lists the most frequently used escape sequences.

The following are examples of calls to puts() and their output:

### Example 1 Input

```c
puts("This is printed with the puts()!");
```

### Example 1 Output

This is printed with the puts() function!

### Example 2 Input

```c
puts("This prints on the first line. \nThis prints on the second line.");
puts("This prints on the third line.");
puts("If these were printf(), all four lines would be on two lines!");
```

### Example 2 Output

```
This prints on the first line.
This prints on the second line.
This prints on the third line.
If these were printf(), all four lines would be on two lines!
```

## # Inputting Numeric Data with scanf()

Just as most programs need to output data to the screen, they also need to input data from the keyboard. The most flexible way your program can read numeric data from the keyboard is by using the `scanf()` function library.

The `scanf()` function reads data from the keyboard according to a specified format and assigns the input to one or more program variables. Like `printf()`, `scanf()` uses a format string to describe the format of the input. The format string utilizes the same conversion specifiers as the `printf()` function. For example, the statement

```c
scanf("%d", &x);
```

reads a decimal from the keyboard and assigns it to the integer variable x. Likewise, the following statement reads a floating-point value from the keyboard and assigns it to the variable `rate`:

```c
scanf("%f", &rate);
```

What is an ampersand (&) before the variable's name? The & is C's `address-of` operator, which is fully explained in Lesson 9, "Understanding Pointers." For now, all you need to remember is that `scanf()` requires the & before numeric variable name in its argument list.

A single `scanf()` can input more than one value if you include multiple conversion specifiers in the format string and variable names (again, each preceded by & in the argument list). The following statement inputs an integer value and a floating-point value and assigns them to the variables x and `rate`, respectively:

```c
scanf("%d %f", &x, &rate);
```

When multiple variables are entered, `scanf()` uses white space to separate input into fields. White space can be spaces, tabs, or newlines. Each conversion specifier in the format string is matched with input field; the end of input field is identified by white space. This gives you considerable flexibility. Be careful when setting up scanf(). If you are looking for a number and the user enters a character, then you might see unexpected results. Unlike other functions, programs that use scanf() must include the stdio.h header file.

### 7.3 Using scanf() to Obtain Values

```c
#include <stdio.h>

int main( void )
{
    int x = 0;
    float rate = 0.0;
    int selection = 0;

    do
    {
        puts("1 - Get a signed integer");
        puts("2 - Get a floating-point number");
        puts("3 - Get an unsigned integer");
        puts("4 - Quit");
        printf("\nEnter a selection:");
        scanf("%d", &selection);
    } while ( selection < 1 || selection > 4);

    if (selection == 1)
    {
        printf("Enter a signed integer:");
        scanf("%d", &x);
        printf("\Your values are: int: %d\n", x);
    }
    else if (selection == 2)
    {
        printf("Enter a floating-point number:");
        scanf("%f", &rate);
        printf("\Your values are: float: %f\n", rate);
    }
    else if (selection == 3)
    {
        printf("Enter an unsigned integer:");
        scanf("%u", &x);
        printf("\Your values are: unsigned: %u\n", x);
    }

    return 0;
}
```
