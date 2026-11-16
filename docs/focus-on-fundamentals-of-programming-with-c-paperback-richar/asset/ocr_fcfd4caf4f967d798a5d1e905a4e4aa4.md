C provides a wide range of types. The most common are:

| int | represents a whole number |
| float | represents a floating point (real) number |
| double | represents a floating point (real) number |
| char | represents a single byte of memory, enough to hold a character |

There are also several variants on these types:

| short | represents an integer, possibly of reduced range |
| long | represents an integer, possible of increased range |
| unsigned | an integer with no negative range |
| unsigned long | like unsigned, possible of increased range |

All of the integer types plus the `char` are called the integral types. `float` and `double` are called the real types.

As said previously, all C program variables must be declared, or associated with a data type, before they are used in a program. This serves four purposes:

+   - Data types define the amount of storage that must be allocated for each variable.
+   - Data types define the interpretation given to each storage location.
+   - Data types define the range of values a variable may take.
+   - Data types define a set of operations that may be performed on the variable.

# Integer Data Types

Integers, or `int` in C, can represent whole numbers that do not have a fractional component such as 1, 10, -35, 450, 11232, etc. Commas or blanks are never used to represent integers. Integer variables should be used where the numeric value will not have a fractional component, such as in counting, etc.

The table below indicates the number of bytes allocated for variables of each data type along with the range of values that can be held by a variable of each data type.