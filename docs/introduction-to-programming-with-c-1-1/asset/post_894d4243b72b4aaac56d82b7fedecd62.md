
Real or Floating point constants – Example: 0.0, 1203.03, 30486.184

Octal & Hexadecimal constants – Example: octal: (013 )₈ = (11)₁₀, Hexadecimal: (013)₁₆ = (19)₁₀

Character constants - Example: ‘a’, ‘A’, ‘z’

String constants - Example: “GeeksforGeeks”

**Strings:** Strings are nothing but an array of characters ended with a null character (‘\0’). This null character indicates the end of the string. Strings are always enclosed in double quotes. Whereas, a character is enclosed in single quotes in C and C++. **Declarations for String:**

- char string[20] = {‘g’, ‘e’, ‘e’, ‘k’, ‘s’, ‘f’, ‘o’, ‘r’, ‘g’, ‘e’, ‘e’, ‘k’, ‘s’, ‘\0’};
- char string[20] = “geeksforgeeks”;
- char string [] = “geeksforgeeks”;

## Difference between above declarations are:

when we declare char as “string[20]”, 20 bytes of memory space is allocated for holding the string value.

When we declare char as “string[]”, memory space will be allocated as per the requirement during execution of the program

**Special Symbols:** The following special symbols are used in C having some special meaning and thus, cannot be used for some other purpose.[] () {} , ; * = #

**Brackets[]:** Opening and closing brackets are used as array element reference. These indicate single and multidimensional subscripts.

**Parentheses():** These special symbols are used to indicate function calls and function parameters.

**Braces{}:** These opening and ending curly braces marks the start and end of a block of code containing more than one executable statement.

**comma (, ):** It is used to separate more than one statements like in for loop is separates initialization, condition and increment.

**semi colon :** It is an operator that essentially invokes something called an initialization list.

**asterick (*):** It is used to create pointer variable.

**assignment operator:** It is used to assign values.

**pre processor(#):** The preprocessor is a macro processor that is used automatically by the compiler to transform your program before actual compilation.

**Operators:** Operators are symbols that triggers an action when applied to C variables and other objects. The data items on which operators act upon are called operands. Depending on the number of operands that an operator can act upon, operators can be classified as follows:

**Unary Operators:** Those operators that require only single operand to act upon are known as unary operators. For Example increment and decrement operators

**Binary Operators:** Those operators that require two operands to act upon are called binary operators. **Binary operators are classified into :**

- 1. Arithmetic operators
- 2. Relational Operators
- 3. Logical Operators
- 4. Assignment Operators
- 5. Conditional Operators
- 6. Bitwise Operators

**Ternary Operators:** These operators requires three operands to act upon. For Example Conditional operator(?:).

# Variables and Keywords in C

A **variable** in simple terms is a storage place which has some memory allocated to it. So basically a variable used to store some form of data. Different types of variables require different amounts of memory and have some specific set of operations which can be applied on them.

**Variable Declaration:**
A typical variable declaration is of the form:

```
type variable_name;
or for multiple variables:
type variable1_name, variable2_name, variable3_name;
```

A variable name can consist of alphabets (both upper and lower case), numbers and the underscore ` _ ` character. However, the name must not start with a number.

# Difference b/w variable declaration and definition

Variable declaration refers to the part where a variable is first declared or introduced before its first use. Variable definition is the part where the variable is assigned a memory location and a value. Most of the times, variable declaration and definition are done together

See the following C program for better clarification:

```
```c
#include <stdio.h>
int main()
{
    // declaration and definition of variable 'a123'
    char a123 = 'a';
    // This is also both declaration and definition as 'b' is allocated
    // memory and assigned some garbage value.
    float b;
    // multiple declarations and definitions
    int _c, _d45, e;
    // Let us print a variable
    printf("%c \n", a123);
    return 0;
}
```
```

**Output:**

a

**Keywords** are specific reserved words in C each of which has a specific feature associated with it. Almost all of the words which help us use the functionality of the C language are included in the list of keywords. So you can imagine that the list of keywords is not going to be a small one!

There are a total of 32 keywords in C:

- auto    break    case    char    const    continue  
- default    do    double    else    enum    extern  
- float    for    goto    if    int    long  
- register    return    short    signed    sizeof    static  
- struct    switch    typedef    union    unsigned    void  
- volatile    while

const: const can be used to declare constant variables. Constant variables are variables which when initialized, can’t change their value. Or in other words, the value assigned to them is unmodifiable.

Syntax:

```
```c
const data_type var_name = var_value;
```
```

Note: Constant variables need to be compulsorily be initialized during their declaration itself. const keyword is also used with pointers. Please refer the [const qualifier in C](#) for understanding the same.

**static:** static keyword is used to declare static variables which are popularly used while writing programs in C language. Static variables have a property of preserving their value even after they are out of their scope! Hence, static variables preserve the value of their last use in their scope. So we can say that they are initialized only once and exist till the termination of the program. Thus, no new memory is allocated because they are not re-declared. Their scope is local to the function to which they were defined. Global static variables can be accessed anywhere in the program. By default, they are assigned the value 0 by the compiler.

Syntax:

```
static data_type var_name = var_value;
```

# How are variables scoped in C – Static or Dynamic?

In C, variables are always statically (or lexically) scoped i.e., binding of a variable can be determined by program text and is independent of the run-time function call stack.

For example, output for the below program is 0, i.e., the value returned by f() is not dependent on who is calling it. f() always returns the value of global variable x.

```
int x = 0;
int f()
{
    return x;
}
int g()
{
    int x = 1;
    return f();
}
int main()
{
    printf("%d", g());
    printf("\n");
    getchar();
}
```

# Scope rules in C

Scope of an identifier is the part of the program where the identifier may directly be accessible. In C, all identifiers are lexically (or statically) scoped. C scope rules can be covered under following two categories.

# Global Scope: Can be accessed anywhere in a program.

```
// filename: file1.c
int a;
int main(void)
{
  a = 2;
}
// filename: file2.c
// When this file is linked with file1.c, functions of this file can access a
extern int a;
int myfun()
{
  a = 2;
}
```

To restrict access to current file only, global variables can be marked as static.

# Block Scope: A Block is a set of statements enclosed within left and right braces ({ and } respectively). Blocks may be nested in C (a block may contain other blocks inside it). A variable declared in a block is accessible in the block and all inner blocks of that block, but not accessible outside the block.

What if the inner block itself has one variable with the same name? If an inner block declares a variable with the same name as the variable declared by the outer block, then the visibility of the outer block variable ends at the pint of declaration by inner block.

```
int main()
{
  {
    int x = 10, y = 20;
    {
      // The outer block contains declaration of x and y, so
      // following statement is valid and prints 10 and 20
      printf("x = %d, y = %d\n", x, y);
      {
        // y is declared again, so outer block y is not accessible
        // in this block
        int y = 40;
```
