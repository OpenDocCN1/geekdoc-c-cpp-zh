
```
8;
3 + 4;
```

However, these statements do nothing for your program and can’t really be considered sensible statements. More typically, statements change values and call functions:

```
x = 25;
++x;
y = sqrt(x);
```

Although a statement (or, at least, a sensible statement) is a complete instruction, not all complete instructions are statements. Consider the following statement:

```
x = 6 + (y = 5);
```

In it, the subexpression y = 5 is a complete instruction, but it is only part of the statement. Because a complete instruction is not necessarily a statement, a semicolon is needed to identify instructions that truly are statements.

So far you have encountered five kinds of statements (not counting the null statement). Listing 5.13 gives a short example that uses all five.

### Listing 5.13 The addemup.c Program

```c
/* addemup.c -- five kinds of statements */
#include <stdio.h>
int main(void)                /* finds sum of first 20 integers */
{
    int count, sum;            /* declaration statement          */

    count = 0;                 /* assignment statement           */
    sum = 0;                   /* ditto                          */
    while (count++ < 20)       /* while                          */
        sum = sum + count;     /* statement                      */
    printf("sum = %d\n", sum); /* function statement             */

    return 0;                  /* return statement               */
}
```

Let’s discuss Listing 5.13. By now, you must be pretty familiar with the declaration statement. Nonetheless, we will remind you that it establishes the names and type of variables and causes memory locations to be set aside for them. Note that a declaration statement is not an expression statement. That is, if you remove the semicolon from a declaration, you get something that is not an expression and that does not have a value:

```c
int port                    /* not an expression, has no value */
```

The assignment statement is the workhorse of many programs; it assigns a value to a variable. It consists of a variable name followed by the assignment operator (=) followed by an expression followed by a semicolon. Note that this particular while statement includes an assignment statement within it. An assignment statement is an example of an expression statement.

A function statement causes the function to do whatever it does. In this example, the printf() function is invoked to print some results. A while statement has three distinct parts (see Figure 5.6). First is the keyword while. Then, in parentheses, is a test condition. Finally, you have the statement that is performed if the test is met. Only one statement is included in the loop. It can be a simple statement, as in this example, in which case no braces are needed to mark it off, or the statement can be a compound statement, like some of the earlier examples, in which case braces are required. You can read about compound statements just ahead.

![](img/c84b77d4534c72b32b9d7ca8ee81bf4c_198_0.png)

Figure 5.6 Structure of a simple while loop.

The while statement belongs to a class of statements sometimes called structured statements because they possess a structure more complex than that of a simple assignment statement. In later chapters, you will encounter many other kinds of structured statements.

The return statement terminates the execution of a function.

## Side Effects and Sequence Points

Now for a little more C terminology: A side effect is the modification of a data object or file. For instance, the side effect of the statement

```c
states = 50;
```

is to set the states variable to 50. Side effect? This looks more like the main intent! From the standpoint of C, however, the main intent is evaluating expressions. Show C the expression 4 + 6, and C evaluates it to 10. Show it the expression states = 50, and C evaluates it to 50. Evaluating that expression has the side effect of changing the states variable to 50. The increment and decrement operators, like the assignment operator, have side effects and are used primarily because of their side effects.

Similarly, when you call the printf() function, the fact that it displays information is a side effect. (The value of printf(), recall, is the number of items displayed.)

A sequence point is a point in program execution at which all side effects are evaluated before going on to the next step. In C, the semicolon in a statement marks a sequence point. That means all changes made by assignment operators, increment operators, and decrement operators in a statement must take place before a program proceeds to the next statement. Some operators that we’ll discuss in later chapters have sequence points. Also, the end of any full expression is a sequence point.

What’s a full expression? A full expression is one that’s not a subexpression of a larger expression. Examples of full expressions include the expression in an expression statement and the expression serving as a test condition for a while loop.

Sequence points help clarify when postfix incrementation takes place. Consider, for instance, the following code:

```c
while (guests++ < 10)
    printf("%d \n", guests);
```

Sometimes C newcomers assume that “use the value and then increment it” means, in this context, to increment guests after it’s used in the printf() statement. However, the guests++ < 10 expression is a full expression because it is a while loop test condition, so the end of this expression is a sequence point. Therefore, C guarantees that the side effect (incrementing guests) takes place before the program moves on to printf(). Using the postfix form, however, guarantees that guests will be incremented after the comparison to 10 is made.

Now consider this statement:

```c
y = (4 + x++) + (6 + x++);
```

The expression 4 + x++ is not a full expression, so C does not guarantee that x will be incremented immediately after the subexpression 4 + x++ is evaluated. Here, the full expression is the entire assignment statement, and the semicolon marks the sequence point, so all that C guarantees is that x will have been incremented twice by the time the program moves to the following statement. C does not specify whether x is incremented after each subexpression is evaluated or only after all the expressions have been evaluated, which is why you should avoid statements of this kind.

## Compound Statements (Blocks)

A compound statement is two or more statements grouped together by enclosing them in braces; it is also called a block. The shoes2.c program used a block to let the while statement encompass several statements. Compare the following program fragments:

```c
/* fragment 1 */
index = 0;
while (index++ < 10)
    sam = 10 * index + 2;
printf("sam = %d\n", sam);
```

```c
/* fragment 2 */
index = 0;
while (index++ < 10)
{
    sam = 10 * index + 2;
    printf("sam = %d\n", sam);
}
```

In fragment 1, only the assignment statement is included in the while loop. In the absence of braces, a while statement runs from the while to the next semicolon. The printf() function will be called just once, after the loop has been completed.

In fragment 2, the braces ensure that both statements are part of the while loop, and printf() is called each time the loop is executed. The entire compound statement is considered to be the single statement in terms of the structure of a while statement (see Figure 5.7).

![](img/c84b77d4534c72b32b9d7ca8ee81bf4c_200_0.png)

Figure 5.7 A while loop with a compound statement.

## Type Conversions

Statements and expressions should normally use variables and constants of just one type. If, however, you mix types, C doesn’t stop dead in its tracks the way, say, Pascal does. Instead, it uses a set of rules to make type conversions automatically. This can be a convenience, but it can also be a danger, especially if you are mixing types inadvertently. (The lint program, found on many Unix systems, checks for type “clashes.” Many non-Unix C compilers report possible type problems if you select a higher error level.) It is a good idea to have at least some knowledge of the type conversion rules.

The basic rules are

- 1. When appearing in an expression, char and short, both signed and unsigned, are automatically converted to int or, if necessary, to unsigned int. (If short is the same size as int, unsigned short is larger than int; in that case, unsigned short is converted to unsigned int.) Under K&R C, but not under current C, float is automatically converted to double. Because they are conversions to larger types, they are called promotions.
- 2. In any operation involving two types, both values are converted to the higher ranking of the two types.
- 3. The ranking of types, from highest to lowest, is long double, double, float, unsigned long long, long long, unsigned long, long, unsigned int, and int. One possible exception is when long and int are the same size, in which case unsigned int outranks long. The short and char types don’t appear in this list because they would have been already promoted to int or perhaps unsigned int.
- 4. In an assignment statement, the final result of the calculations is converted to the type of the variable being assigned a value. This process can result in promotion, as described in rule 1, or demotion, in which a value is converted to a lower-ranking type.
- 5. When passed as function arguments, char and short are converted to int, and float is converted to double. This automatic promotion is overridden by function prototyping, as discussed in Chapter 9, “Functions.”

Promotion is usually a smooth, uneventful process, but demotion can lead to real trouble. The reason is simple: The lower-ranking type may not be big enough to hold the complete number. For instance, an 8-bit char variable can hold the integer 101 but not the integer 22334.

What happens when the converted value won’t fit into the destination? The answer depends on the types involved. Here are the rules for when the assigned value doesn’t fit into the destination type:

- 1. When the destination is some form of unsigned integer and the assigned value is an integer, the extra bits that make the value too big are ignored. For instance, if the destination is 8-bit unsigned char, the assigned value is the original value modulus 256.
