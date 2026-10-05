
func = pick;

Here is a concrete example:

```c
#include <stdio.h>
#include <string.h>

// forward declaration for the check function
// the third parameter is a function pointer
void check(char *a, char *b, int (*cmp)(const char *, const char *));

int main(void)
{
    char s1[80] = "hello world";
    char s2[80] = "bye";

    // declare a function pointer
    int (*p)(const char *, const char *);

    // assign strcmp function to p
    p = strcmp;
    check(s1, s2, p);
    return 0;
}

void check(char *a, char *b, int (*cmp)(const char *, const char *))
{
    printf("Testing for equality.\n");

    if (cmp(a, b))
        printf("Equal");
    else
        printf("Not Equal");
}
```

implementation of check function

The check() function is called, two pointers and one function pointer are passed as arguments. Inside check(), the expression (*cmp)(a, b) calls strcmp(), which is pointed to by cmp, with arguments a and b.

## C Language: setjmp and longjmp

The functions setjmp() and longjmp() can be used to save the execution context of program and restore it at some later point. By execution context, we mean the state of CPU registers, the stack and allocated memory. setjmp() saves the execution context of the program and longjmp() restores it.

setjmp() and longjmp() can be used to jump to different parts of program. Practical uses include jumping out of deeply nested loops, invoking error handling and jumping to named labels. All of this is explained with example:

```c
#include <setjmp.h>
#include <stdio.h>

void jumper(jmp_buf env) {
    printf("inside jumper\n");
    longjmp(env, 1);
    printf("after longjmp\n");
}

int main() {
    jmp_buf env;
    int ret = setjmp(env);
    if (ret == 0) {
        printf("setjmp executed\n");
    } else {
        printf("returned from longjmp\n");
        return 1;
    }
    jumper(env);
    return 0;
}
```

output:
setjmp executed
inside jumper

## The goto Statement

The C and C++ goto keyword is implemented with setjmp and longjmp. goto allows us to jump to a program label:

```c
#include <setjmp.h>
#include <stdio.h>

int main() {
    printf("hello world\n");
    goto foo_label;
    printf("1+1=2\n");

foo_label:
    printf("goodbye\n");
    return 0;
}
```

output:
hello world
goodbye

## C Language: typedef

We can define new names for existing data types by using the keyword typedef. With typedef we are not actually creating a new data type, but rather defining a new name for an existing type.

typedef can help make machine-dependent programs more portable. If we define our type name for each machine-dependent data type used by our program, then only the typedef statements have to be changed when compiling the program on machines with different architectures.

typedef has syntax:

```c
typedef old_type_name new_type_name;
```

For example:

```c
typedef float balance;
```

balance is just another name for the type float; now that balance is defined as a type, we can do:

```c
balance over_due;
```

over_due is a variable of type balance.

## C Language: Enumerations

An enumeration is a user-defined type whose values are confined to a set of named integer constants. A variable of such a type can only have a value that is equal to one of the named integer constants that are specified by this type.

The syntax for enumerations is:

```c
enum enum_name { enumeration list } variable_list;
```

Both the enum name and the variable list are optional. Here is an example:

```c
enum FILETYPE { FILE_NONE, FILE_C, FILE_ASM, FILE_OBJ } FileType;
```

The key point to understand about an enumeration is that each of the symbols in the enumeration list is an integer value. As such, they may be used anywhere that an integer can be used. Each symbol is given a value that is one greater than the symbol that precedes it. The value of the first enumeration symbol is 0.

Here is an example:

```c
enum coin { penny, nickel, dime, quarter, half_dollar, dollar };
```

```c
enum coin money
```

enum coin is an enumeration type and money is a variable of type enum coin. Note that the type is enum coin, not coin. In C++, an enumeration name is a complete type, so we can declare the variable money as:

```cpp
coin money
```

We can also declare enumerations with specific enum values:

```c
enum coin {penny, nickel, dime, quarter, half_dollar, dollar};
```

| penny | 0 |
|---|---|
| nickel | 1 |
| dime | 2 |
| quarter | 3 |
| half_dollar | 4 |
| dollar | 5 |

## Anonymous Enums

An anonymous enum is defined as follows:

```c
enum { COLOR };
```

This is the same as int except we cannot get the address of. This is very useful when we define const. The anonymous enum is effectively a compile-time constant.

## C Language: size_t And sizeof

size_t is an unsigned integer type. It is defined in <stdio.h> and <stdlib.h>. size_t is used to represent the size of objects. It is the return type of the sizeof operator. size_t is guaranteed to be big enough to hold the largest integer that host system can handle. The maximum permissible size is dependent on compiler. If the compiler is 32 bit then size_t is simply unsigned int and if the compiler is 64 bit then size_t is unsigned long long. The size_t data type is never negative.

## Compile Time Operator sizeof

sizeof is a unary operator that returns the length in bytes of variable or parenthesized type that it precedes.

```c
double f;
printf("%d", sizeof(f));
printf("%d", sizeof(int));
printf("%d", sizeof(double));
printf("%d", sizeof(struct Employee));
```

The operand of sizeof is a native C or C++ type then must be enclosed in parentheses. sizeof primarily helps to generate portable code that depends upon the size of built-in data types.

Structures and unions can be used to create variables of different sizes. The actual size of these variables may change from machine to machine. The sizeof operator computes the size of any variable or type and can help eliminate machine-dependent code from our programs. This operator is especially useful where structures or unions are concerned.
