
## Chapter 7 Loops

The **while** construct is similar to the **if** construct, but with one major difference: In the **if** construct, if the expression is true, the block of code is run once. In the **while** construct, the block is run again and again until the expression becomes false.

Rewrite the **main()** function to look like this:

```c
#include <stdio.h>

int main(int argc, const char * argv[])
{
    int i = 0;
    while (i < 12) {
        printf("%d. Aaron is Cool\n", i);
        i++;
    }
    return 0;
}
```

Build and run the program.

The conditional (`i < 12`) is being checked before each execution of the block. The first time it evaluates to false, execution leaps to the code after the block.

Notice that the second line of the block increments `i`. This is important. If `i` wasn’t incremented, then this loop, as written, would continue forever because the expression would always be true. Here’s a flow-chart of this while loop:

![](img/5f9368899ebf8d92fc145f8def1e89f8_60_0.png)

### The for loop

The **while** loop is a general looping structure, but C programmers use the same basic pattern a lot: `some initialization while (some check) { some code some last step }`

So, the C language has a shortcut: the **for** loop. In the **for** loop, the pattern shown above becomes:

```c
for (some initialization; some check; some last step) {
    some code;
}
```

Change the program to use a **for** loop:

```c
#include <stdio.h>

int main(int argc, const char * argv[])
{
    for (int i = 0; i < 12; i++) {
        printf("%d. Aaron is Cool\n", i);
    }
    return 0;
}
```

**Figure 7.2 for loop**

![](img/5f9368899ebf8d92fc145f8def1e89f8_61_0.png)

Note that in this simple loop example, you used the loop to dictate the number of times something happens. More commonly, however, loops are used to *iterate* through a collection of items, such as a list of names. For instance, I could modify this program to use a loop in conjunction with a list of friends’ names. Each time through the loop, a different friend would get to be cool. We’ll see more of collections and loops starting in Chapter 15.

### break

Sometimes it is necessary to stop the loop’s execution from the inside the loop. For example, let’s say you want to step through the positive integers looking for the number *x*, where *x + 90 = x²*. Your plan is to step through the integers 0 through 11 and pop out of the loop when you find the solution. Change the code:

```c
#include <stdio.h>

int main(int argc, const char * argv[])
{
    int i;
    for (i = 0; i < 12; i++) {
        printf("Checking i = %d\n", i);
        if (i + 90 == i * i) {
            break;
        }
    }
    printf("The answer is %d.\n", i);
    return 0;
}
```

Build and run the program. You should see:

```text
Checking i = 0
Checking i = 1
Checking i = 2
Checking i = 3
Checking i = 4
Checking i = 5
Checking i = 6
Checking i = 7
Checking i = 8
Checking i = 9
Checking i = 10
The answer is 10.
```

Notice that when **break** is called execution skips directly to the end of the code block.

**Figure 7.3 Breaking out of a loop**

![](img/5f9368899ebf8d92fc145f8def1e89f8_62_0.png)

### continue

Sometimes you will find yourself in the middle of the code block, and you need to say, “Forget the rest of this run through the code block and start the next run through the code block.” This is done with the **continue** command. For example, what if you were pretty sure that no multiples of 3 satisfied the equation? How would you avoid wasting precious time checking those?

```c
#include <stdio.h>

int main(int argc, const char * argv[])
{
    int i;
    for (i = 0; i < 12; i++) {
        if (i % 3 == 0) {
            continue;
        }
        printf("Checking i = %d\n", i);
        if (i + 90 == i * i) {
            break;
        }
    }
    printf("The answer is %d.\n", i);
    return 0;
}
```

Build and run it:

```text
Checking i = 1
Checking i = 2
Checking i = 4
Checking i = 5
Checking i = 7
Checking i = 8
Checking i = 10
The answer is 10.
```

![](img/5f9368899ebf8d92fc145f8def1e89f8_63_0.png)

### The do-while loop

None of the cool kids use the **do-while** loop, but for completeness, here it is. The **do-while** loop doesn't check the expression until it has executed the block. Thus, it ensures that the block is always executed at least once. If you rewrote the original exercise to use a **do-while** loop, it would look like this:

```c
int main(int argc, const char * argv[]) 
{
    int i = 0;
    do {
        printf("%d. Aaron is Cool\n", i);
        i++;
    } while (i < 13);
    return 0;
}
```

Notice the trailing semicolon. That’s because unlike the other loops, a **do-while** loop is actually one long statement:

```text
do { something } while ( something else stays true );
```

Here’s a flow-chart of this do-while loop:

![](img/5f9368899ebf8d92fc145f8def1e89f8_64_0.png)

### Challenge

Write a program that counts backward from 99 through 0 by 3, printing each number. However, if the number is divisible by 5, it should also print the words “Found one!”. Thus, the output should look something like this:

```text
99
96
93
90
Found one!
87
...
0
Found one!
```

## Addresses and Pointers

Your computer is, at its core, a processor (the Central Processing Unit or CPU) and a vast meadow of switches (the Random-Access memory or RAM) that can be turned on or off by the processor. We say that a switch holds one *bit* of information. You’ll often see 1 used to represent “on” and 0 used to represent “off.”

Eight of these switches make a *byte* of information. The processor can fetch the state of these switches, do operations on the bits, and store the result in another set of switches. For example, the processor might fetch a byte from here and another byte from there, add them together, and store the result in a byte way over someplace else.

![](img/5f9368899ebf8d92fc145f8def1e89f8_65_0.png)

The memory is numbered, and we typically talk about the *address* of a particular byte of data. When people talk about a 32-bit CPU or a 64-bit CPU, they are usually talking about how big the address is. A 64-bit CPU can deal with much, much more memory than a 32-bit CPU.

### Getting addresses

In Xcode, create a new project: a C Command Line Tool named **Addresses**.

The address of a variable is the location in memory where the value for that variable is stored. To get the variable’s address, you use the `&` operator:

```c
#include <stdio.h>

int main(int argc, const char * argv[])
{
    int i = 17;
    printf("i stores its value at %p\n", &i);
    return 0;
}
```

Notice the `%p` token. That's the token you can replace with a memory address. Build and run the program. You'll see something like:

```text
i stores its value at 0xbffff738
```

although your computer may put `i` at a completely different address. Memory addresses are nearly always printed in hexadecimal format.

In a computer, everything is stored in memory, and thus everything has an address. For example, a function starts at some particular address. To get that address, you just use the function's name:

```c
int main(int argc, const char * argv[])
{
    int i = 17;
    printf("i stores its value at %p\n", &i);
    printf("this function starts at %p\n", main);
    return 0;
}
```

Build and run the program.

### Storing addresses in pointers

What if you wanted to store an address in a variable? You could stuff it into an unsigned integer that was the right size, but the compiler will help you catch your mistakes if you are more specific when you give that variable its type. For example, if you wanted a variable named `ptr` that holds the address where a float can be found, you would declare it like this:

```c
float *ptr;
```

We say that `ptr` is a variable that is a *pointer* to a float. It doesn't store the value of a float; it points to an address where a float may be stored.

Declare a new variable named `addressOfI` that is a pointer to an `int`. Assign it the address of `i`.

```c
int main(int argc, const char * argv[])
{
    int i = 17;
    int *addressOfI = &i;
    printf("i stores its value at %p\n", addressOfI);
    printf("this function starts at %p\n", main);
    return 0;
}
```

Build and run the program. You should see no change in its behavior.

We're using integers right now to be simple. But if you're wondering what the point of pointers is, I hear you. It would be just as easy to pass the integer value assigned to this variable as it is to pass its address. Soon, however, your data will be much larger and much more complex than single integers. That's why we pass addresses. It's not always possible to pass a copy of data you want to work with, but you can always pass the *address* of where that data begins. And it's easy to access data once you have its address.
