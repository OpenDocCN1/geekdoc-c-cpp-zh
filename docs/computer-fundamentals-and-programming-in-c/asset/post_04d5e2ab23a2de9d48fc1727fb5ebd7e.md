
![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_163_0.png)

C provides a standard, minimal set of basic data types. Sometimes these are called 'primitive' types. More complex data types can be built up from these basic types. C has five basic data types (Refer Fig. 8.8) and they are as follows:

- character—Keyword used is char
- integer—Keyword used is int
- floating-point—Keyword used is float
- double precision floating point—Keyword used is double
- valueless—Keyword used is void

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_163_1.png)

Table 8.2(a) lists the sizes and ranges of basic data types in C for a 16-bit computer and Table 8.2(b) lists the sizes and ranges of basic data types in C for a 32-bit computer.

Table 8.2(a) Sizes and ranges of basic data types in C for a 16-bit computer

| Data type | Size (in bits) | Range |
|---|---|---|
| char | 8 | -128 to 127 |
| int | 16 | -32768 to 32767 |
| float | 32 | 1.17549 × 10^-38 to 3.40282 × 10^38 |
| double | 64 | 2.22507 × 10^-308 to 1.79769 × 10^308 |
| void | 8 | valueless |

Table 8.2(b) Sizes and ranges of basic data types in C for a 32-bit computer

| Data type | Size (in bits) | Range |
|---|---|---|
| char | 8 | -128 to 127 |
| int | 32 | -2147483648 to 2147483647 |
| float | 32 | 1.17549 × 10^-38 to 3.40282 × 10^38 |
| double | 64 | 2.22507 × 10^-308 to 1.79769 × 10^308 |
| void | 8 | valueless |

The C standard does not state how much precision the float and double types provide, since different computers may store floating point numbers in different ways. According to IEEE, the precisions for float and double are 6 and 15, respectively.

The void type has no values and only one operation, assignment. The void type specifies an empty set of values. It is used as the type returned by functions that generate no value. The void type never refers to an object and therefore, is not included in any reference to object types. According to ISO/IEC draft, 'The void type comprises an empty set of values; it is an incomplete type that cannot be completed.'

In addition, C has four type specifiers or modifiers and three type qualifiers.

The following points should be noted:

- (a) Each of these type of modifiers can be applied to the base type int.
- (b) The modifiers signed and unsigned can also be applied to the base type char.
- (c) In addition, long can be applied to double.
- (d) When the base type is omitted from a declaration, int is assumed.
- (e) The type void does not have these modifiers.

The specifiers and qualifiers for the data types can be broadly classified into three types:

- Size specifiers—short and long
- Sign specifiers—signed and unsigned
- Type qualifiers—const, volatile, and restrict

The size qualifier alters the size of the basic data types. There are two such qualifiers that can be used with the data type int; these are short and long.

The specifier short, when placed in front of the int declaration, tells the C compiler that the particular variable being declared is used to store fairly small integer values. The motivation for using short variables is primarily of conserving memory space, which can be an issue in situations in which the program needs a lot of memory and the amount of available memory is limited.

In any ANSI C compiler, the sizes of short int, int, and long int are restricted by the following rules:

- The minimum size of a short int is two bytes.
- The size of an int must be greater than or equal to that of a short int.
- The size of a long int must be greater than or equal to that of an int.
- The minimum size of a long int is four bytes.

In most of the DOS based compilers that work on 16-bit computers, the size of a short int and an int is the same, which is two bytes. In such compilers, a long int occupies four bytes. On the other hand, in the 32-bit machine compilers such as GNU C (gcc), int and long int take four bytes while a short int occupies two bytes. For UNIX based compilers, a short int takes two bytes, while a long int takes four bytes.

The long qualifier is also used with the basic data type double. In older compilers, this qualifier was used with float, but it is not allowed in the popular compilers of today. As mentioned earlier, it may be noted here that the sign qualifiers can be used only with the basic data types int and char.

Table 8.3 lists the sizes of the short int, int and long int data types in different machines.

Table 8.3 Sizes in number of bytes of the short int, int and long int data types in different machines.

| | 16-bit machine | 32-bit machine | 64-bit machine |
|---|---|---|---|
| short int | 2 | 2 | 2 |
| int | 2 | 4 | 4 |
| long int | 4 | 4 | 8 |

C99 provides two additional integer types: long long int and unsigned long long int. For long long, the C99 standard specified at least 64 bits to support. Table 8.4 summarizes the size and range of different variations of long long type.

Table 8.4 Size and range of long long type

| | Size (in bytes) | Range |
|---|---|---|
| long long int | 8 | - 9223372036854775808 to + 9223372036854775807 |
| unsigned long int or unsigned long | 4 | 0 to 4294967295 |
| unsigned long long int or unsigned long long | 8 | 0 to + 18446744073709551615 |

The C89 Committee added to C two type qualifiers, const and volatile; and C99 adds a third, restrict. Type qualifiers control the way variables may be accessed or modified. They specify the variables that will never (const) change and those variables that can change unexpectedly (volatile).

Both keywords require that an associated data type be declared for the identifier, for example,

```c
const float pi = 3.14156;
```

specifies that the variable pi can never be changed by the program. Any attempt by code within the program to alter the value of pi will result in a compile time error. The value of a const variable must be set at the time the variable is declared. Specifying a variable as const allows the compiler to perform better optimization on the program because of the data type being known. Consider the following program:

```c
#include <stdio.h>
int main(void)
{
    const int value = 42;
    /* constant, initialized integer variable */
    value = 100;
    /* wrong! - will cause compiler error */
    return 0;
}
```

### Note

- const does not turn a variable into a constant. A variable with const qualifier merely means the variable cannot be used for assignment. This makes the value read only through that variable; it does not prevent the value from being modified in some other ways, e.g., through a pointer.

The volatile keyword indicates that a variable can unexpectedly change because of events outside the control of the program. This is usually used when some variable within the program is linked directly with some hardware component of the system. The hardware could then directly modify the value of the variable without the knowledge of the program. For example, an I/O device might need to write directly into a program or data space. Meanwhile, the program itself may never directly access the memory area in question. In such a case, we would not want the compiler to optimize-out this data area that never seems to be used by the program, yet must exist for the function to correctly work in a larger context. It tells the compiler that the object is subject to sudden change for reasons which cannot be predicted from a study of the program itself, and forces every reference to such an object to be a genuine reference.

The restrict type qualifier allows programs to be written so that translators can produce significantly faster executables. Anyone for whom this is not a concern can safely ignore this feature of the language.

Size and range of different combinations of basic data types and modifiers are listed in Table 8.5.

Several new types that were added in C89 are listed below:

- void
- void*
- signed char
- unsigned char
- unsigned short
- unsigned long
- long double

Moreover, new designations for existing types were added in C89:

- signed short for short
- signed int for int
- signed long for long
