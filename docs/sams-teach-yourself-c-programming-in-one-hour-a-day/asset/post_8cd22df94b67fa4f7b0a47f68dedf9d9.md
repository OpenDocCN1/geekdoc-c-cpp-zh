
# LESSON 5 Packaging Code in Functions

> CAUTION: If you try to use a function with a void return type as an expression, the compiler generates an error message.

| DO | DON'T |
|---|---|
| DO pass parameters to functions to make the function generic and thus reusable. | DON'T make an individual statement confusing by putting a bunch of functions in it. You should put functions into your statements only if they don't make the code more confusing |
| DO take advantage of the ability to put functions into expressions. | |

# Recursion

The term recursion refers to a situation in which a function calls itself either directly or indirectly. Indirect recursion occurs when one function calls another function that calls the first function. C allows recursive functions, and they can be useful in some situations.

For example, recursion can be used to calculate the factorial of a number. The factorial of a number x is written x! and is calculated as follows:

```
x! = x * (x-1) * (x-2) * (x-3) * ... * (2) * 1
```

However, you can also calculate x! like this:

```
x! = x * (x-1) !
```

Going one step further, you can calculate (x-1)! using the same procedure:

```
(x-1)! = (x-1) * (x-2) !
```

You continue calculating recursively until you're down to a value of 1, in which case you're finished. The program in Listing 5.5 uses a recursive function to calculate factorials. Because the program uses unsigned integers, it's limited to an input value of 8; the factorial of 9 and larger values are outside the allowed range for integers.

# LISTING 5.5 recurse.C; Using a Recursive Function to Calculate Factorials

```c
/* Demonstrates function recursion. Calculates the
 * factorial of a number. */
#include <stdio.h>
unsigned int f, x;
unsigned int factorial(unsigned int a);

int main(void) {
    puts("Enter an integer value between 1 and 8: ");
    scanf("%d", &x);
    if (x > 8 || x < 1) {
        printf("Only values from 1 to 8 are acceptable!");
    } else {
        f = factorial(x);
        printf("%u factorial equals %u\n", x, f);
    }
    return 0;
}

unsigned int factorial(unsigned int a) {
    if (a == 1) {
        return 1;
    } else {
        a *= factorial(a-1);
    }
}
```

# Output

Enter an integer value between 1 and 8:
6
6 factorial equals 720

# Analysis ▼

The first half of this program is like many of the other programs you have worked with so far. It starts with comments on lines 1 and 2. On line 4, the appropriate header file is included for the input/output routines. Line 6 declares a couple of unsigned integer values. Line 7 is a function prototype for the factorial function. Notice that it takes unsigned int as its parameter and returns an unsigned int. Lines 9 through 25 are the main() function. Lines 11 and 12 print a message asking for a value from 1 to 8 and then accept an entered value.

Lines 14 through 22 show an interesting if statement. Because a value greater than 8 causes a problem, this if statement checks the value. If it's greater than 8, an error message is printed; otherwise, the program figures the factorial on line 20 and prints the result on line 21. When you know there could be a problem, such as a limit on the size of a number, add code to detect the problem and prevent it.

The recursive function, factorial(), is located on lines 27 through 36. The value passed is assigned to a. On line 29, the value of a is checked. If it's 1, the program returns the value of a. If the value isn't 1, a is set equal to times the value of factorial(a-1). The program calls the factorial function again, but this the value of a is (a-1). If (a-1) isn't equal to 1, factorial() is called again with ((a-1), which is the same as (a-2). This process continues until the if statement on line 29 is true. If the value of the factorial is 3, the factorial is evaluated to the:

```
3 * (3-1) * ((3-1)
```

| DO | DON'T |
|---|---|
| understand and work with recursion before you use it in a program you are going to distribute. | DON'T use recursion if there will be several iterations. (An iteration is the repetition of a program statement.) Recursion uses many resources because the function has to remember where it is. |

# Where the Functions Belong

You might be wondering in your source code you should place your function definitions. For now, they should go in the same source code file as main() and after the end of main().

You can keep your user-defined functions in a separate source-code file, apart from main(). This technique is useful with large programs and when you want to use the same set of functions in more than one program. This technique is discussed in Lesson 22, "Advanced Compiler Use."

# Working with Inline Functions

There is a special type of function that can be created in C. These are inline functions. Inline functions are generally small functions. When the compiler executes, it tries to execute an inline function in the fastest manner possible. This may be done by copying the function's code into the calling function. it is called inline.

A function made inline by using the inline keyword. The following declares an inline function called toInches:

```c
inline int toInches( int Feet )
{
  return (Feet*12);
}
```

When the toInches function is used, the compiler will do its best to optimize it to be fast. Be although that the general assumption is that the compiler will simply be moved into the calling function, this is not a guarantee. The only guarantee is that the compiler will do its best to optimize the code of it in this function. You can use inline functions like any other.

# Summary

This lesson introduced you to functions, an important part of C. Functions are independent sections of code that perform tasks. When your program needs a task performed it calls the function that performs that task. The use of functions is essential for structured programming—a method of program design that emphasizes a modular, top-down approach.

You also learned that a function consists of a header and a body. The header includes information about the function's return type, name, and parameters. The body contains local variable declarations and the statements that are executed when the function is called. Finally, you saw that local variables—those declared within a function—are totally independent of any other variables.

# Q&A

Q What if I need to return more than one value from a function?

A Many times you will need to return more than one value from a function, or more commonly, you will want to change a value you send to the function and keep the change after the function ends. This process is covered in Lesson 19, "Getting More from Functions."

Q How do I know what a good function name is?

A Effective function naming is similar to effective variable naming. A good function name describes as specifically as possible what the function does.

Q When variables are declared at the top of the listing, before main(), they can be used anywhere, but local variables can be used only in the specific function. Why not just declare everything before main()?

A Variable scope is discussed in more detail in Lesson 12. You will learn why it is better to declare variables locally within functions instead of globally.

Q What other ways are there to use recursion?

A factorial function is a prime example of using recursion. The factorial number is needed in many statistical calculations. Recursion is just a loop; however, it has one difference from other loops. With recursion, each time a recursive function is called, a new set of variables is created. This is not true of the other loops.

Q Does main() have to be the first function in a program?

A. It is a standard in C that the main() function is the first function to execute; however, it can be placed anywhere in your source file. Most people place it first or last so that it's easy to locate

# Workshop

The Workshop provides quiz questions to help you solidify your understanding of the material covered and exercises to provide you with experience in using what you've learned.

# Quiz

+   1. Will you use structured programming when writing your C programs?

+   2. How does structured programming work?

+   3. How do C functions fit into structured programming?
