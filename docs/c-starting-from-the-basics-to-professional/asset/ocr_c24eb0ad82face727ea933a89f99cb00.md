Because `fish_count` is an integer, you are not allowed to specify a precision for that field. And so this invocation of `std::format()`, and by extension your entire program, will fail when executed.

Even though we only explain how to handle exceptions in Chapter 16, you need a means to debug failing `std::format()` statements. After all: you will be using `std::format()` in examples and exercises long before Chapter 16, and finding out which tiny little mistake you made in a format specifier can be tricky at times. Hence, the following tip:

> > **Tip**  To debug a failing `std::format()` expression, you can put the corresponding statement inside a so-called try-catch block as follows (this code is available in `Ex2_03D.cpp`):

```
```cpp
try
{
    std::cout << std::format("Pond diameter required for {:.2f} fish is {:.2f} feet.\n",
                             fish_count, pond_diameter);
}
catch (const std::format_error& error)
{
    std::cout << error.what();  // Outputs "precision not allowed for this argument type"
}
```
```

The program will now no longer fail and instead will output a diagnostic message that should aid you in fixing the buggy format specifier. This try-catch snippet uses several language elements you do not know yet (references, exceptions, etc.), but you can easily copy-paste it from `Ex2_03D.cpp` whenever you need it.

# ## Formatting Tabular Data

The following formatting options (highlighted in black) allow you to control the width and alignment of each field. We regularly use them in this book to output text that resembles a table.

```
`[[fill]align][sign][#][0][width][.precision][type]`
```

`width` is a positive integer that defines the *minimum field width*. If needed, extra characters are inserted into the formatted field to reach this minimum width. Which characters are inserted and where depends both on the fill style and which other formatting options are present:

+   - For numeric fields, if the width option is preceded with a `0` (zero), extra `0` characters are inserted before the number's digits, but after any sign character (`+` or `-`) or prefix sequence (such as `0x` for hexadecimal numbers; see later).
+   - Otherwise, the so-called *fill character* is inserted. The default fill character is a space, but you can override this with the fill formatting option. The align option determines where this fill character is inserted. A field can be *left-aligned* (`<`), *right-aligned* (`>`), or *centered* (`^`). The default alignment depends on the field's type.

You cannot specify the fill character without specifying an alignment as well. Note also that the fill, align, and `0` options have no effect unless you also specify a width.