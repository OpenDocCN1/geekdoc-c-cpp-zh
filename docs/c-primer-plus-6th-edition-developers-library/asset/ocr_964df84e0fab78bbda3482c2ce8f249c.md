| Modifier | Meaning |
|---|---|
| t | Used with an integer conversion specifier to indicate a `ptrdiff_t` value. This is the type corresponding to the difference between two pointers. (C99).
|  | Examples: `"%td"` and `"%12ti"`. |
| z | Used with an integer conversion specifier to indicate a `size_t` value. This is the type returned by `sizeof`. (C99).
|  | Examples: `"%zd"` and `"%12zx"`. |

# Note Type Portability

The `sizeof` operator, recall, returns the size, in bytes, of a type or value. This should be some form of integer, but the standard only provides that it should be an unsigned integer. Thus it could be `unsigned int`, `unsigned long`, or even `unsigned long long`. So, if you were to use `printf()` to display a `sizeof` expression, you might use `%u` on one system, `%lu` one another, and `%llu` on a third. This means you would need to research the correct usage for your system and that you might need to alter your program if you move it to a different system. Well, it would have meant that except that C provides help to make the type more portable. First, the `stddef.h` header file (included when you include `stdio.h`) defines `size_t` to be whatever the type your system uses for `sizeof`; this is called the underlying type. Second, `printf()` uses the `z` modifier to indicate the corresponding type for printing. Similarly, C defines the `ptrdiff_t` type and `t` modifier to indicate whatever underlying signed integer type the system used for the difference between two addresses.

# Note Conversion of float Arguments

There are conversion specifiers to print the floating types `double` and `long double`. However, there is no specifier for `float`. The reason is that `float` values were automatically converted to type `double` before being used in an expression or as an argument under K&R C. ANSI C (or later), in general, does not automatically convert `float` to `double`. To protect the enormous number of existing programs that assume `float` arguments are converted to `double`, however, all `float` arguments to `printf()`—as well as to any other C function not using an explicit prototype—are still automatically converted to `double`. Therefore, under either K&R C or ANSI C, no special conversion specifier is needed for displaying type `float`.

# Table 4.5 The printf() Flags

| Flag | Meaning |
|---|---|
| - | The item is left-justified; that is, it is printed beginning at the left of the field. |
|  | Example: `"%-20s"`. |