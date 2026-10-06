
Constants can be of any of the basic data types like an integer constant, a floating constant, a character constant, or a string literal. There are enumeration constants as well.

Constants are treated just like regular variables except that their values cannot be modified by their definition.

## Integer Literals

An integer literal can be a decimal, octal, or hexadecimal constant. A prefix specifies the base or radix: 0x or 0X for hexadecimal, 0 for octal, and nothing for decimal.

An integer literal also have a suffix that is a combination of U and L, for unsigned and long, respectively. The suffix can be uppercase or lowercase and can be in any order.

Here are some examples of integer literals.

```
212 /* Legal */
215u /* Legal */
0FeeL /* Legal */
078 /* Illegal: 8 is not an octal digit */
032UU /* Illegal: cannot repeat a suffix */
```

Following are other examples of various types of integer literals.

```
85 /* decimal */
0213 /* octal */
0x4b /* hexadecimal */
30 /* int */
30u /* unsigned int */
30l /* long */
30ul /* unsigned long */
```

## Floating-point Literals

A floating-point literal has an integer part, a decimal part, a fractional part, and an exponent part. You can represent floating point literals either in decimal form or exponential form.

While representing decimal form, you must include the decimal point, the exponent, or both; and while representing exponential form, you must include the integer part, the fractional part, or both. The signed exponent is introduced by e or E.

Here are some examples of floating-point literals.

| 3.14159 | /* Legal */ |
| 314159-SL | /* Legal */ |
| 510E | /* Illegal: incomplete exponent */ |
| 210f | /* Illegal: no decimal or exponent */ |
| .55 | /* Illegal: missing integer or fraction */ |

## Character Constants

Character literals are enclosed in single quotes, e.g., 'x' can be stored in a simple variable of char type.

A character literal can be a plain character (e.g., 'x'), an escape sequence (e.g., '\t'), or a universal character (e.g., '\u02C0').

There are certain characters in C that represent special meaning when preceded by a backslash for example, newline(\n) or tab (\t).

Following is the example to show a few escape sequence characters.

```
#include <stdio.h>

int main() {
    printf("Hello\tWorld\n\n");
    return 0;
}
```

When the code is compiled and executed, it produces the following result:

Hello World

## String Literals

String literals or constants are enclosed in double quotes "\". A string contains characters that are similar to character literals: plain characters, escape sequences, and universal characters.

You can break a long line into multiple lines using string literals and separating whitespaces.

Here are some examples of string literals. All the three forms are identical strings.

```
"hello, dear"
"hello, \
dear"
"hello, "d" "ear"
```

## Defining Constants

There are two simple ways in C to define constants:

- Using **define** preprocessor.
- Using **const** keyword.

## #define Preprocessor

Given below is the form to use #define preprocessor to define a constant.

##define identifier value

The following example explains it in detail.

```
#include<stdio.h>

#define LENGTH 10
#define WIDTH 5
#define NEWLINE '\n'

int main(){
int area;

area= LENGTH * WIDTH;
printf("value of area : %d", area);
printf("%c", NEWLINE);

return 0;
}
```

When the above code is compiled and executed, it produces the following result:
value of area : 50

## The const Keyword

You can use const prefix to declare constants with a specific type as follows:
`const type variable = value;`

The following example explains it in detail.

```
#include<stdio.h>
int main(){
const int LENGTH =10;
const int WIDTH =5;
const char NEWLINE = "\n";
int area;
area=LENGTH * WIDTH;
printf("value of area : %d", area);
printf("%c", NEWLINE);

return 0;
}
```

When the above code is compiled and executed, it produces the following result:
value of area : 50

## VARIABLES

In programming, a variable is a container (storage area) to hold data.
To indicate the storage area, each variable should be given a unique name (identifier). Variable names are just the symbolic representation of a memory location.

For example:

- 1. int marks=95;

Here, marks is a variable of int type. Here, the variable is assigned an integer value 95.

## Rules to Name a Variable

- 1. Variable name must not start with a digit.
2. Variable name can consist of alphabets, digits and special symbols underscore_.
3. Blank or spaces are not allowed in variable name.
4. Keywords are not allowed as variable name.
5. Upper and lower case names are treated as different.

## Declaring, Defining and Initializing a Variable

Declaring a variable means informing the compiler that the variable exists. Declaration does the following:

1. It tells the compiler the variable name.
2. It specifies what type of data the variable will hold.
3. Until the variable is defined, the compiler has to worry about allocating memory space to the variable.
4. A variable is declared using keyword, outside the main() function.

```
int a;
float b;
double c;
```

Defining a variable means to assign storage to the variable. You can define it inside the function and use it. We can even define multiple variables of same type in a single line by using comma to separate them.

```
int a;
float b,c;
```

Initializing a variable means to provide it with a value. A variable can be initialized in a single statement, like:

```
int a=5;
```

## Difference between Variable and Identifier

An Identifier is a name given to any variable, function, structure, pointer or any other entity in a programming language. A variable is a named memory location to store data.

| Identifier | Variable |
| --- | --- |
| Identifier is the name given to a variable, function, etc. | While, variable is used to name a memory location which stores data. |
| An identifier can be a variable, but not all identifiers are variables. | All variable names are identifiers. |

Example:

```
// a variable
int a;
or, a function
int a() {
}
```

Example:
// int variable
int a;
// float variable
float a and b, i.e, float b,c;

Another great analogy to understand the difference between Identifier and Variable is:

You can think of an Identifier x to be a variable's name, but it can also be a function's name int() { } and still be an identifier.

Just like vasavi is a name of a person, but also the name of a foundation.

## Scope and Life of Variables in C

Lifetime: Lifetime of any variable is the time for which the particular variable outlives in memory during running of the program.

Scope: The scope of any variable is actually a subset of lifetime. A variable may be in the memory but may not be accessible though, the area of our program where we can actually access our variable is the scope of that variable.

The scope of any variable can be broadly categorized into three categories:

- Global scope: When variable is defined outside all functions. It is then available to all the functions of the program and all the blocks program contains.
- Local scope: When variable is defined inside a function or a block, then it is locally accessible within the block and hence it is a local variable.
