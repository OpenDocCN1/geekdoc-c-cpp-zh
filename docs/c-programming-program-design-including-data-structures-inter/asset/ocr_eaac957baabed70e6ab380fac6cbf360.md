the size of memory makes for one less thing to think about. To effectively use memory, a programmer can look at the type of data to be used by a program and thereby figure out which data type to use. (Memory constraints may still be a concern for programs written for applications such as a wristwatch.)

Newer programming languages have only five categories of simple data types: integer, real, char, bool, and the enumeration type. The integral data types that are used in this book are int, bool, and char.

Table 2-2 gives the range of possible values associated with these three data types and the size of memory allocated to manipulate these values.

**TABLE 2-2** Values and Memory Allocation for Three Simple Data Types

| Data Type | Values | Storage (in bytes) |
|---|---|---|
| int | -2147483648 to 2147483647 | 4 |
| bool | true and false | 1 |
| char | -128 to 127 | 1 |

> > **NOTE**
> >
> > Use this table only as a guide. Different compilers may allow different ranges of values. Check your compiler's documentation. To find the exact size of the integral data types on a particular system, you can run a program given in Appendix G (Memory Size of a System). Furthermore, to find the maximum and minimum values of these data types, you can run another program given in Appendix F (Header File cllimits).

> > **NOTE**
> >
> > To deal with large integers, the new standard of C++ introduces the data type long long. The memory space for a long long data value is 64 bytes and the range of values belonging to this data type is -9223372036854775808 (−2^63) to 9223372036854775807 (2^63 − 1).

# ### `int` DATA TYPE

This section describes the int data type. This discussion also applies to other integral data types.

Integers in C++, as in mathematics, are numbers such as the following:

−6728, −67, 0, 78, 36782, +763