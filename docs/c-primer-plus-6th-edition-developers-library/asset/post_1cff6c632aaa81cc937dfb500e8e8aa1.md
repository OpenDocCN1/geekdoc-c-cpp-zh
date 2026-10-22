
When we tried to compile Listing 9.5, our compiler gave an error message stating that the call to imax() had too few parameters.

What about the type errors? To investigate those, we replaced imax(3) with imax(3, 5) and tried compilation again. This time there were no error messages, and we ran the program. Here is the resulting output:

```
The maximum of 3 and 5 is 5.
The maximum of 3 and 5 is 5.
```

As promised, the 3.0 and 5.0 of the second call were converted to 3 and 5 so that the function could handle the input properly.

Although it gave no error message, our compiler did give a warning to the effect that a double was converted to int and that there was a possible loss of data. For example, the call

```
imax(3.9, 5.4)
```

becomes equivalent to the following:

```
imax(3, 5)
```

The difference between an error and a warning is that an error prevents compilation and a warning permits compilation. Some compilers make this type cast without telling you. That’s because the standard doesn’t require warnings. However, many compilers enable you to select a warning level that controls how verbose the compiler will be in issuing warnings.

## No Arguments and Unspecified Arguments

Suppose you give a prototype like this:

```
void print_name();
```

An ANSI C compiler will assume that you have decided to forego function prototyping, and it will not check arguments. To indicate that a function really has no arguments, use the void keyword within the parentheses:

```
void print_name(void);
```

ANSI C interprets the preceding expression to mean that print_name() takes no arguments. It then checks to see that you, in fact, do not use arguments when calling this function.

A few functions, such as printf() and scanf(), take a variable number of arguments. In printf(), for example, the first argument is a string, but the remaining arguments are fixed in neither type nor number. ANSI C allows partial prototyping for such cases. You could, for example, use this prototype for printf():

```
int printf(const char *, ...);
```

## Recursion Revealed

To see what’s involved, let’s look at an example. The function main() in Listing 9.6 calls the up_and_down() function. We’ll term this the “first level of recursion.” Then up_and_down() calls itself; we’ll call that the “second level of recursion.” The second level calls the third level, and so on. This example is set up to go four levels. To provide an inside look at what is happening, the program not only displays the value of the variable n, it also displays &n, which is the memory address at which the variable n is stored. (This chapter discusses the & operator more fully later. The printf() function uses the %p specifier for addresses. If your system doesn’t support that format, try %u or %lu.)

### Listing 9.6 The recur.c Program

```
/* recur.c -- recursion illustration */
#include <stdio.h>
void up_and_down(int);

int main(void)
{
    up_and_down(1);
    return 0;
}

void up_and_down(int n)
{
    printf("Level %d: n location %p\n", n, &n); // 1
    if (n < 4)
        up_and_down(n+1);
    printf("LEVEL %d: n location %p\n", n, &n); // 2
}
```

The output on one system looks like this:

```
Level 1: n location 0x0012ff48
Level 2: n location 0x0012ff3c
Level 3: n location 0x0012ff30
Level 4: n location 0x0012ff24
LEVEL 4: n location 0x0012ff24
LEVEL 3: n location 0x0012ff30
LEVEL 2: n location 0x0012ff3c
LEVEL 1: n location 0x0012ff48
```

Let’s trace through the program to see how recursion works. First, main() calls up_and_down() with an argument of 1. As a result, the formal parameter n in up_and_down() has the value 1, so print statement #1 prints Level 1. Then, because n is less than 4, up_and_down() (Level 1) calls up_and_down() (Level 2) with an actual argument of n + 1, or 2. This causes n in the

Second, each function call is balanced with a return. When program flow reaches the return at the end of the last recursion level, control passes to the previous recursion level. The program does not jump all the way back to the original call in main(). Instead, the program must move back through each recursion level, returning from one level of up_and_down() to the level of up_and_down() that called it.

Third, statements in a recursive function that come before the recursive call are executed in the same order that the functions are called. For example, in Listing 9.6, print statement #1 comes before the recursive call. It was executed four times in the order of the recursive calls: Level 1, Level 2, Level 3, and Level 4.

Fourth, statements in a recursive function that come after the recursive call are executed in the opposite order from which the functions are called. For example, print statement #2 comes after the recursive call, and it was executed in the order: Level 4, Level 3, Level 2, Level 1. This feature of recursion is useful for programming problems involving reversals of order. You'll see an example soon.

Fifth, although each level of recursion has its own set of variables, the code itself is not duplicated. The code is a sequence of instructions, and a function call is a command to go to the beginning of that set of instructions. A recursive call, then, returns the program to the beginning of that instruction set. Aside from recursive calls creating new variables on each call, they are much like a loop. Indeed, sometimes recursion can be used instead of loops, and vice versa.

Finally, it's vital that a recursive function contain something to halt the sequence of recursive calls. Typically, a recursive function uses an if test, or equivalent, to terminate recursion when a function parameter reaches a particular value. For this to work, each call needs to use a different value for the parameter. For example, in the last example, up_and_down(n) calls up_and_down(n+1). Eventually, the actual argument reaches the value 4, causing the if (n < 4) test to fail.

## Tail Recursion

In the simplest form of recursion, the recursive call is at the end of the function, just before the return statement. This is called tail recursion, or end recursion, because the recursive call comes at the end. Tail recursion is the simplest form because it acts like a loop.

Let's look at both a loop version and a tail recursion version of a function to calculate factorials. The factorial of an integer is the product of the integers from 1 through that number. For example, 3 factorial (written 3!) is 1*2*3. Also, 0! is taken to be 1, and factorials are not defined for negative numbers. Listing 9.7 presents one function that uses a for loop to calculate factorials and a second that uses recursion.

### Listing 9.7 The factor.c Program

```
// factor.c -- uses loops and recursion to calculate factorials
#include <stdio.h>
long fact(int n);
long rfact(int n);
int main(void)
{
    int num;

    printf("This program calculates factorials.\n");
    printf("Enter a value in the range 0-12 (q to quit):\n");
    while (scanf("%d", &num) == 1)
    {
        if (num < 0)
            printf("No negative numbers, please.\n");
        else if (num > 12)
            printf("Keep input under 13.\n");
        else
        {
            printf("loop: %d factorial = %ld\n",
                num, fact(num));
            printf("recursion: %d factorial = %ld\n",
                num, rfact(num));
        }
        printf("Enter a value in the range 0-12 (q to quit):\n");
    }
    printf("Bye.\n");

    return 0;
}

long fact(int n)    // loop-based function
{
    long ans;

    for (ans = 1; n > 1; n--)
        ans *= n;

    return ans;
}

long rfact(int n)   // recursive version
{
    long ans;
    if (n > 0)
        ans= n * rfact(n-1);
    else
        ans = 1;

    return ans;
}
```

The test driver program limits input to the integers 0–12. It turns out that 12! is slightly under half a billion, which makes 13! much larger than long on our system. To go beyond 12!, you would have to use a type with greater range, such as double or long long.

Here’s a sample run:

```
This program calculates factorials.
Enter a value in the range 0-12 (q to quit):
5
loop: 5 factorial = 120
recursion: 5 factorial = 120
Enter a value in the range 0-12 (q to quit):
10
loop: 10 factorial = 3628800
recursion: 10 factorial = 3628800
Enter a value in the range 0-12 (q to quit):
q
Bye.
```

The loop version initializes ans to 1 and then multiplies it by the integers from n down to 2. Technically, you should multiply by 1, but that doesn’t change the value.

Now consider the recursive version. The key is that n! = n × (n−1)!. This follows because (n−1)! is the product of all the positive integers through n−1. Therefore, multiplying by n gives the product through n. This suggests a recursive approach. If you call the function rfact(), rfact(n) is n * rfact(n−1). You can thus evaluate rfact(n) by having it call rfact(n−1), as in Listing 9.7. Of course, you have to end the recursion at some point, and you can do this by setting the return value to 1 when n is 0.

The recursive version of Listing 9.7 produces the same output as the loop version. Note that although the recursive call to rfact() is not the last line in the function, it is the last statement executed when n > 0, so it is tail recursion.

Given that you can use either a loop or recursion to code a function, which should you use? Normally, the loop is the better choice. First, because each recursive call gets its own set of variables, recursion uses more memory; each recursive call places a new set of variables on the stack. And space restrictions in the stack can limit the number of recursive calls. Second, recursion is slower because each function call takes time. So why show this example? Because tail recursion is the simplest form of recursion to understand, and recursion is worth understanding because in some cases, there is no simple loop alternative.

## Recursion and Reversal

Now let’s look at a problem in which recursion’s ability to reverse order is handy. (This is a case for which recursion is simpler than using a loop.) The problem is this: Write a function that prints the binary equivalent of an integer. Binary notation represents numbers in terms of powers of 2. Just as 234 in decimal means 2 × 10² + 3 × 10¹ + 4 × 10⁰, so 101 in binary means 1 × 2² + 0 × 2¹ + 1 × 2⁰. Binary numbers use only the digits 0 and 1.
