
## `char` Constants

C treats `char` constants as type `int`, and C++ treats them as type `char`. For instance, consider this statement:

```
```c
char ch = 'A';
```
```

In C, the constant `'A'` is stored in an int-sized chunk of memory; more precisely, the character code is stored in the `int`. The same numeric value is also stored in the variable `ch`, but here it occupies just one byte of memory.

C++, on the other hand, uses one byte for `'A'`, as well as for `ch`. This distinction doesn’t affect any of the examples in this text. However, some C programs do make use of char constants being type `int` by using character notation to represent integer values. For instance, if a system has a 4-byte `int`, you can do this in C:

```
```c
int x = 'ABCD';  /* ok in C for 4-byte int but not for C++ */
```
```

The meaning of `'ABCD'` is a 4-byte `int` in which the first byte stores the character code for the letter A, the second byte stores the character code for B, and so on. Note that `'ABCD'` is something quite different from "ABCD". The former is just a funny way of writing an `int` value, but the latter is a string and corresponds to the address of a 5-byte chunk of memory.

Consider the following code:

```
```c
int x = 'ABCD';
char c = 'ABCD';
printf("%d %d %c %c\n", x, 'ABCD', c, 'ABCD');
```
```

On our system, it produces this output:

```
```text
1094861636 1094861636 D D
```
```

This example illustrates that if you treat `'ABCD'` as an `int`, it is a 4-byte integer value, but if you treat it as type char, the program looks only at the final byte. Attempt to print `'ABCD'` by using the `%s` specifier caused the program to crash on our system, because the numeric value of `'ABCD'` (1094861636) was an out-of-bounds address.

The rationale for using values such as `'ABCD'` is that it provides a means to set each byte in the `int` independently, because each character corresponds exactly to one byte. However, a better approach, because it doesn’t depend on particular character codes, is to use hexadecimal values for integer constants, using the fact that each two-digit hexadecimal group corresponds to one byte. Chapter 15, “Bit Fiddling,” discusses this technique. (Early versions of C didn’t provide hexadecimal notation, which probably is why the multicharacter constant technique was developed in the first place.)

## The `const` Modifier

In C, a global `const` has external linkage, but in C++, it has internal linkage. That is, the C++ declaration

```
const double PI = 3.14159;
```

is equivalent to the C declaration

```
static const double PI = 3.14159;
```

provided both declarations are outside of any function. The C++ rule has the goal of making it simpler to use const in header files. If the constant has internal linkage, each file that includes the header file gets its own copy of the constant. If a constant has external linkage, one file has to have a defining declaration and the other files have to have a reference declaration, one that uses the keyword extern.

Incidentally, C++ can use the keyword extern to make a const value have external linkage, so both languages can create constants with internal linkage and external linkage. The difference is just in which kind of linkage is used by default.

One additional property of the C++ const is that it can be used to declare the size of an ordinary array:

```
const int ARSIZE = 100;
double loons[ARSIZE];  /* in C++, same as double loons[100];  */
```

You can make the same declarations in C99, but in C99, the declaration creates a variable array.

In C++, but not in C, you can use const values to initialize other const values:

```
const double RATE = 0.06;        // valid C++, C
const double STEP = 24.5;        // valid C++, C
const double LEVEL = RATE * STEP;  // valid C++, invalid C
```

## Structures and Unions

After you declare a structure or union having a tag, you can use the tag as a type name in C++:

```
struct duo
{
    int a;
    int b;
};
struct duo m;  /* valid C, C++ */
duo n;        /* invalid C, valid C++ */
```

As a result, a structure name can conflict with a variable name. For example, the following program compiles as a C program, but it fails as a C++ program because C++ interprets duo in the printf() statement as a structure type rather than as the external variable:

```
#include <stdio.h>
float duo = 100.3;
int main(void)
{
    struct duo { int a; int b;};
```

```
int * pi;
void * pv;
pv = ar;          /* ok in C, C++ */
pi = pv;          /* ok in C, invalid in C++ */
pi = (int * ) pv; /* ok in C, C++ */
```

Another difference in C++ is that you can assign the address of a derived-class object to a base-class pointer, but that relates to features that don’t even exist in C.

## Boolean Types

In C++, the Boolean type is bool, and true and false are keywords. In C, the Boolean type is _Bool, but including the header file stdbool.h makes bool, true, and false available.

## Alternative Spellings

In C++, the alternative spellings of or for ||, and so on, are keywords. In C99 and C11, they are defined as macros, and you need to include iso646.h to make them available.

## Wide-Character Support

In C++, wchar_t is a built-in type, and wchar_t is a keyword. In C99 and C11, the wchar_t type is defined in several header files (stddef.h, stdlib.h, wchar.h, wctype.h). Similarly, char16_t and char32_t are C++11 keywords but are macros defined in uchar.h in C11.

C++ provides wide-character I/O support (wchar_t, char16_t, and char32_t) through the iostream header file, whereas C99 provides a completely different package of I/O support through the wchar.h header file.

## Complex Types

C++ supports complex types through a complex class provided by the complex header file. C has built-in complex types and supports them through the complex.h header file. The two approaches are quite different and are not compatible with one another. The C version reflects a greater concern with the needs and practices of the numerical computation community.

## Inline Functions

C99 has added inline function support, a feature C++ already had. However, the C99 implementation is more flexible. In C++, an inline function has internal linkage by default. If a C++ inline function appears in more than one file, it has to have the same definition, using the same tokens. For example, one file can’t have a definition using a type int parameter and another file have a definition using a type int32_t parameter, even if int32_t is a typedef for int. C, however, allows that arrangement. Also, C, as described in Chapter 15, allows a mixture of inline and external definitions that C++ doesn’t allow.

## C99/11 Features Not Found in C++11

Although C traditionally is more or less a subset of C++, the C99 standard adds several features missing in C++. Here are some of the more prominent C99/C11-only features:

- Designated initializers
- Compound initializers
- Restricted pointers
- Variable-length arrays
- Flexible array members
- Macros with a variable number of arguments

Note
This list is just a snapshot at one particular time, and the lists of shared and unshared features will continue to evolve. For example, C++14 adds a feature similar to the C99 variable-length array.

## Index

## Symbols

-/+ (sign operators), 149

[ ] (brackets), 102

arrays, 384

empty, 388, 424

%= assignment operator, 214

*= assignment operator, 214, 230

+= assignment operator, 214

-= assignment operator, 214

/= assignment operator, 214

~ bitwise operator, 688

<< (left shift) bitwise operator, 684

>> (right shift) bitwise operator, 684-685

. (period) character, 262

* modifier, printf( ) function, 133-135

! operator, 264

# operator, strings from macro arguments, 721-722

## operator, 722-723

& operator, 367-368

bitwise, 679

&& operator, 264

ranges, 267-268

| operator, bitwise, 679-680

|| operator, 264

+ (addition) operator, 149

= (assignment) operator, 146-149, 202

?: (conditional) operator, 272-273

– (decrement) operator, 164-166
