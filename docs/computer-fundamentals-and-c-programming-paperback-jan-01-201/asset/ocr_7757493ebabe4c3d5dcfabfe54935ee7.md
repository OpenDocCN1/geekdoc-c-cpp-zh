By now, you should be comfortable in using `printf` conversion codes and their modifiers. We’ll thus focus on the field width, precision and flags in the rest of this chapter. But before doing that, let’s take up a program which demonstrates some of the features that have been discussed.

**TABLE 9.3** Format Specifiers and Flags Used by `printf`

| Integer | short | int | long | long long |
|---|---|---|---|---|
| Signed Decimal | `%hd` | `%d, %i` | `%ld` | `%lld` (C99) |
| Unsigned Decimal | `%hu` | `%u` | `%lu` | `%llu` (C99) |
| Octal | `%ho` | `%o` | `%lo` | `%llo` (C99) |
| Hex | `%hx` | `%x` | `%lx` | `%llx` (C99) |
| Floating Point | float | double | long double | |
| Normal | `%f` | `%f` | `%Lf` | |
| Exponential | `%e, %E` | `%le, %lE` | `%Le, %LE` | |
| Exponential or normal | `%g, %G` | `%lg, %lG` | `%Lg, %LG` | |
| Other Format Specifiers | Prints | | | |
| `%c` | Character (char) | | | |
| `%s` | Character string (not restricted to one word) | | | |
| `%p` | Pointer | | | |
| `%n` | Nothing, but saves count of printed characters in a variable. | | | |
| `%%` | | | | |
| Flag | Significance | | | |
| `-` | Left-justifies output. | | | |
| `+` | Prefixes a + to a non-negative number. | | | |
| Space | Prefixes a space to a non-negative number. | | | |
| `#` | Depends on conversion code:<br>With o, prepends 0 to number.<br>With x/X, prepends 0x or 0X to number.<br>With g/G, prints trailing zeroes.<br>With e/E/f/F/g/G, prints number with decimal point. | | | |
| `0` | Pads field with zeroes when its size is less than field width. | | | |
| `*` | Field width specified by corresponding argument. | | |

# 9.12.3 `printf` special.c: A Second Look at the Data Types

This three-part program (Program 9.9) demonstrates some features of `printf` that may have been overlooked previously. The first part creates two overflow situations and shows the consequences of using an unequal number of arguments and format specifiers. An extra specifier in the first `printf` shows a value of zero, but i2 has been printed only once in the second `printf` statement. The compiler may issue two warnings here.