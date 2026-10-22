
Here is the sample output:

```
Some number limits for this system:
Biggest int: 2147483647
Smallest long long: -9223372036854775808
One byte = 8 bits on this system.
Largest double: 1.797693e+308
Smallest normal float: 1.175494e-38
float precision = 6 digits
float epsilon = 1.192093e-07
```

The C preprocessor is a useful, helpful tool, so take advantage of it when you can. We’ll show you more applications as you move along through this book.

## Exploring and Exploiting printf() and scanf()

The functions printf() and scanf() enable you to communicate with a program. They are called input/output functions, or I/O functions for short. They are not the only I/O functions you can use with C, but they are the most versatile. Historically, these functions, like all other functions in the C library, were not part of the definition of C. C originally left the implementation of I/O up to the compiler writers; this made it possible to better match I/O to specific machines. In the interests of compatibility, various implementations all came with versions of scanf() and printf(). However, there were occasional discrepancies between implementations. The C90 and C99 standards describe standard versions of these functions, and we’ll follow that standard.

Although printf() is an output function and scanf() is an input function, both work much the same, each using a control string and a list of arguments. We will show you how these work, first with printf() and then with scanf().

## The printf() Function

The instructions you give printf() when you ask it to print a variable depend on the variable type. For example, we have used the %d notation when printing an integer and the %c notation when printing a character. These notations are called conversion specifications because they specify how the data is to be converted into displayable form. We’ll list the conversion specifications that the ANSI C standard provides for printf() and then show how to use the more common ones. Table 4.3 presents the conversion specifiers and the type of output they cause to be printed.

Table 4.3 Conversion Specifiers and the Resulting Printed Output

| Conversion | Output Specification |
|------------|----------------------|
| %a | Floating-point number, hexadecimal digits and p-notation (C99/C11). |
| %A | Floating-point number, hexadecimal digits and P-notation (C99/C11). |

```
printf("Farewell! thou art too dear for my possessing,\n");
printf("%c%d\n", '$', 2 * cost);

return 0;
}
```

The output, of course, is

```
The 7 contestants ate 12.750000 berry pies.
The value of pi is 3.141593.
Farewell! thou art too dear for my possessing,
$15600
```

This is the format for using printf():

```
printf(Control-string, item1, item2,...);
```

Item1, item2, and so on, are the items to be printed. They can be variables or constants, or even expressions that are evaluated first before the value is printed. Control-string is a character string describing how the items are to be printed. As mentioned in Chapter 3, the control string should contain a conversion specifier for each item to be printed. For example, consider the following statement:

```
printf("The %d contestants ate %f berry pies.\n", number,
    pies);
```

Control-string is the phrase enclosed in double quotes. This particular control string contains two conversion specifiers corresponding to number and pies—the two items to be displayed. Figure 4.6 shows another example of a printf() statement.

![](img/c84b77d4534c72b32b9d7ca8ee81bf4c_142_0.png)

Figure 4.6 Arguments for printf().

Here is another line from the example:

```
printf("The value of pi is %f.\n", PI);
```

This time, the list of items has just one member—the symbolic constant PI.

As you can see in Figure 4.7, Control-string contains two distinct forms of information:

- Characters that are actually printed
- Conversion specifications

## Caution

Don't forget to use one conversion specification for each item in the list following Control-string. Woe unto you should you forget this basic requirement! Don't do the following:

```
printf("The score was Squids %d, Slugs %d.\n", score1);
```

Here, there is no value for the second %d. The result of this faux pas depends on your system, but at best you will get partial nonsense.

![](img/c84b77d4534c72b32b9d7ca8ee81bf4c_143_0.png)

Figure 4.7 Anatomy of a control string.

If you want to print only a phrase, you don't need any conversion specifications. If you just want to print data, you can dispense with the running commentary. Each of the following statements from Listing 4.6 is quite acceptable:

```
printf("Farewell! thou art too dear for my possessing,\n");
```

```
printf("%c%d\n", '$', 2 * cost);
```

In the second statement, note that the first item on the print list was a character constant rather than a variable and that the second item is a multiplication. This illustrates that printf() uses values, be they variables, constants, or expressions.

Because the printf() function uses the % symbol to identify the conversion specifications, there is a slight problem if you want to print the % sign itself. If you simply use a lone % sign, the compiler thinks you have bungled a conversion specification. The way out is simple—just use two % symbols, as shown here:

```
pc = 2*6;
```

```
printf("Only %d%% of Sally's gribbles were edible.\n", pc);
```

The following output would result:

```
Only 12% of Sally's gribbles were edible.
```

## Conversion Specification Modifiers for printf()

You can modify a basic conversion specification by inserting modifiers between the % and the defining conversion character. Tables 4.4 and 4.5 list the characters you can place there legally. If you use more than one modifier, they should be in the same order as they appear in Table

| Modifier | Meaning |
|---|---|
| t | Used with an integer conversion specifier to indicate a `ptrdiff_t` value. This is the type corresponding to the difference between two pointers. (C99). |
|  | Examples: `"%td"` and `"%12ti"`. |
| z | Used with an integer conversion specifier to indicate a `size_t` value. This is the type returned by `sizeof`. (C99). |
|  | Examples: `"%zd"` and `"%12zx"`. |

## Note Type Portability

The `sizeof` operator, recall, returns the size, in bytes, of a type or value. This should be some form of integer, but the standard only provides that it should be an unsigned integer. Thus it could be `unsigned int`, `unsigned long`, or even `unsigned long long`. So, if you were to use `printf()` to display a `sizeof` expression, you might use `%u` on one system, `%lu` one another, and `%llu` on a third. This means you would need to research the correct usage for your system and that you might need to alter your program if you move it to a different system. Well, it would have meant that except that C provides help to make the type more portable. First, the `stddef.h` header file (included when you include `stdio.h`) defines `size_t` to be whatever the type your system uses for `sizeof`; this is called the underlying type. Second, `printf()` uses the `z` modifier to indicate the corresponding type for printing. Similarly, C defines the `ptrdiff_t` type and `t` modifier to indicate whatever underlying signed integer type the system used for the difference between two addresses.

## Note Conversion of float Arguments

There are conversion specifiers to print the floating types `double` and `long double`. However, there is no specifier for `float`. The reason is that `float` values were automatically converted to type `double` before being used in an expression or as an argument under K&R C. ANSI C (or later), in general, does not automatically convert `float` to `double`. To protect the enormous number of existing programs that assume `float` arguments are converted to `double`, however, all `float` arguments to `printf()`—as well as to any other C function not using an explicit prototype—are still automatically converted to `double`. Therefore, under either K&R C or ANSI C, no special conversion specifier is needed for displaying type `float`.

## Table 4.5 The printf() Flags

| Flag | Meaning |
|---|---|
| - | The item is left-justified; that is, it is printed beginning at the left of the field. |
|  | Example: `"%-20s"`. |
