
two integer values, unless you're lucky, the result is a float — a value with a decimal portion. The solution is to ensure that the values used are float — even when they're whole numbers.

## Exercise 5-13: Rewrite the source code from Listing 5-4 so that the final calculation is made using immediate float values, not integers.

Later in your C journey, you'll learn a trick to typecast calculations, which is a more versatile way to write code that must specify integer values as floats. This topic is covered in Chapter 16.

- Understanding variables
- Creating a specific data type
- Declaring variables in your code
- Using signed or unsigned integers
- Whipping up multiple variables at a time
- Declaring and assigning at the same time
- Putting variables to work
- Creating constants

## Chapter 6

### A Place to Put Stuff

Human beings have obsessed over storing stuff ever since the Garden of Eden, when Adam stashed a grape in his belly button. This raises the question of why Adam would have a belly button, but that’s not my point. My point is that people enjoy storing things and creating places — boxes, closets, garages, and underground bunkers — in which to store stuff.

C programs use three types of values: immediate, constant, and variable. An immediate value is one that you specify in the source code — a value you type. Constants are discussed later in this chapter. Variables are storage containers for values where the contents can change. Their contents can vary — hence the name.

### Setting up a quick example

> Who likes to read a lot about something before they try it? Not me!

Exercise 6-1: Type the source code shown in Listing 6-1. It uses a single variable, x, which is one of the first computer variable names mentioned in the Bible.

```c
#include <stdio.h>
int main()
{
    int x;
    x = 5;
    printf("The value of variable x is %d.\n",x);
    return(0);
}
```

Here's the breakdown of what's going on in Listing 6-1:

Line 5 contains the variable's declaration:

```
int x;
```

All C language variables are declared as a specific data type and assigned a name. The variable in Listing 6-1 is declared as an integer (int) data type and given the name x.

Line 7 assigns the value 5 to variable x:

```
x = 5;
```

The value goes on the right side of the equal sign. The variable goes on the left.

Line 8 uses the variable's value in the printf() statement:

```
printf("The value of variable x is %d.\n",x)
```

The %d conversion character is used because the variable's data type is integer. The conversion character must match the data type.

Build and run the code. The output looks like this:

```
The value of variable x is 5.
```

The following sections describe in further detail the mechanics of creating and using variables.

### Introducing data types

C language variables are designed to hold specific types of data. If C were a biological programming language, cats and dogs would go into the animal data type, and trees and ferns would go into the plant data type. C language variables work along these lines, with specific values assigned to matching types of data.

The common C language data types are listed in Table 6-1.

TABLE 6-1 Basic C Language Variable Types

| Data Type | Description |
|---|---|
| char | Single-character variable; stores one character of information |
| int | Integer variable; stores integer (whole number) values |
| float | Floating-point variable; stores real numbers |
| double | Floating-point variable; stores very large or very small real numbers |
| void | No data type |

When you need to store an integer value, you use a variable of the integer (int) data type. Likewise, if you're storing a letter of the alphabet, you use a variable of the character (char) data type. The program's needs are what determine which data types are required for its variables.

> > The char and int data types store integer values. The char data type has a shorter range, used primarily to store characters — letters of the alphabet, numbers, and symbols — but it can also be used to store small integer values.
> 
> > The float and double data types are both floating-point variables that can store a tiny or huge value or any value with a decimal portion.

> A newer data type, _Bool, stores binary values, 1 or 0, often referred to as TRUE and FALSE, respectively. _Bool, a loaner word from C++, must be written with the initial underscore character and a capital B. You may not find _Bool used in many C program source code listings — most likely, to keep the code compatible with older compilers.

### Using variables

Most, if not all, of your future C language programs will employ variables. Earlier in this chapter, Listing 6-1 illustrates the basic three steps for using variables in the C language:

- 1. Declare the variable, giving it a data type and a name.
- 2. Initialize the variable (assign it a value).
- 3. Use the variable.

All three steps are required for working with variables in your code, and these steps must be completed in that order.

To declare a variable, place a statement near the start of a function, such as the main() function in every C program. Place the declaration after the initial curly bracket. (Refer to Listing 6-1.) The declaration is a statement on a line by itself, ending with a semicolon:

```
type name;
```

type is the data type: char, int, and others are introduced throughout this chapter.

name is the variable's name. The name must not be the name of a C language keyword or any other variable name that was previously declared. The name is case-sensitive — though, traditionally, C language variable names are written in lowercase. If you want to be saucy, you can add numbers or underscores to the variable name, but always start a variable name with a letter.

The equal operator assigns a value to a variable. The format is very specific:

```
variable = value;
```

Read this expression as, “The value of variable equals value.”

variable is the variable's name. It must be declared earlier in the source code.

The value is either an immediate value, a constant, an expression, another variable, or a value returned from a function. After the statement is executed, the variable holds the value that's specified.

Assigning a value to a variable satisfies the second step in using a variable. The third step is to do something with the variable. Variables can be used anywhere in your source code that a value could otherwise be specified directly.

In Listing 6-2, four variable types are declared, assigned values, and used in separate printf() statements.

### Working with Variables

```c
#include <stdio.h>

int main()
{
    char c;
    int i;
    float f;
    double d;

    c = 'a';
    i = 1;
    f = 19.0;
    d = 20000.000;

    printf("%c\n", c);
    printf("%d\n", i);
    printf("%f\n", f);
    printf("%f\n", d);

    return(0);
}
```

Exercise 6-2: Type the source code for Listing 6-2 into the editor. Build and run.

```
a
1
19.000000
20000.000000
```

Your code's output need not look identical to what's shown here.

> » Variables need not be declared at the start of a function. Some programmers declare variables on the line before they're first used. This strategy works, but it's not traditional and can lead to confusion. Most C programmers expect to find all variable declarations at the start of the function.
> 
> » It's possible to start a variable name with an underscore, which the compiler believes to be a letter. Even so, variable names that begin with underscores are used internally in the C language. I recommend avoiding this naming convention.

### Variable Madness!

I hope you're getting the hang of the variable thing. If not, please review the first part of this chapter. The variable is truly the heart of any programming language, by allowing you to code flexibility into your programs and have it do amazing things.

### Using more-specific data types

The C language offers more data types than are shown in Table 6-1. Depending on the information stored, you may want to use one of these more detailed variable declarations. Table 6-2 lists a buffet of C language data types and the range of values those types can store.

The value range column specifies the size of the number you can store in a variable as well as whether negative numbers are allowed. The compiler may not always flag warnings that happen when you assign an incorrect value to a variable type. So get it right when you declare the variable!

For example, if you need to store the value -10, you use a short int, int, or long variable. You cannot use an unsigned int, as the source code in Listing 6-3 demonstrates.
