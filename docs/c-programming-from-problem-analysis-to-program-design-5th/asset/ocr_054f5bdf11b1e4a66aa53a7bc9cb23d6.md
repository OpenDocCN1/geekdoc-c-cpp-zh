Integral data types are further classified into the following nine categories: char, short, int, long, bool, unsigned char, unsigned short, unsigned int, and unsigned long.

Why are there so many categories of the same data type? Every data type has a different set of values associated with it. For example, the char data type is used to represent integers between −128 and 127. The int data type is used to represent integers between −2147483648 and 2147483647, and the data type short is used to represent integers between −32768 and 32767.

Note that the identifier num in Example 2–1 can be assigned any value belonging to the int data type.

Which data type you use depends on how big a number your program needs to deal with. In the early days of programming, computers and main memory were very expensive. Only a small amount of memory was available to execute programs and manipulate the data. As a result, programmers had to optimize the use of memory. Because writing a program and making it work is already a complicated process, not having to worry about the size of the memory makes for one less thing to think about. Thus, to effectively use memory, a programmer can look at the type of data used in a program and figure out which data type to use.

Newer programming languages have only five categories of simple data types: integer, real, char, bool, and the enumeration type. The integral data types that are used in this book are int, bool, and char.

Table 2–2 gives the range of possible values associated with these three data types and the size of memory allocated to manipulate these values.

# TABLE 2-2  Values and Memory Allocation for Three Simple Data Types

| Data Type | Values | Storage (in bytes) |
|---|---|---|
| int | −2147483648 to 2147483647 | 4 |
| bool | true and false | 1 |
| char | −128 to 127 | 1 |

> > **NOTE**  Use this table only as a guide. Different compilers may allow different ranges of values. Check your compiler’s documentation. To find the exact size of the integral data types on a particular system, you can run a program given in Appendix G (Memory Size of a System). Furthermore, to find the maximum and minimum values of these data types, you can run another program given in Appendix F (Header File `<climits>`).